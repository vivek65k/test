  const deepMerge = (target: any, source: any) => {
    const output = { ...target };
    if (typeof target === 'object' && typeof source === 'object') {
      Object.keys(source).forEach(key => {
        if (Array.isArray(source[key])) {
          output[key] = Array.isArray(target[key])
            ? Array.from(new Set([...target[key], ...source[key]]))
            : [...source[key]];
        } else if (
          source[key] &&
          typeof source[key] === 'object' &&
          !Array.isArray(source[key])
        ) {
          output[key] = deepMerge(target[key] || {}, source[key]);
        } else {
          output[key] = source[key];
        }
      });
    }
    return output;
  };

  // Perform deep merge of old + new filters
  const combinedFilters = deepMerge(event.filterDto || {}, filters?.filters || {});
