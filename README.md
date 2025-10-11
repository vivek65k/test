  const oldFilters = this.filters || {};
  const tableFilters = event?.filterDto || {};
  const advFilters = filters?.filters || {};

  // 1️⃣ Merge both filter sources
  const incoming = { ...advFilters, ...tableFilters };

  // 2️⃣ Create new final object
  const updatedFilters: any = {};

  // 3️⃣ Add all valid keys
  Object.entries(incoming).forEach(([key, val]) => {
    if (
      val !== null &&
      val !== undefined &&
      val !== '' &&
      (!Array.isArray(val) || val.length > 0)
    ) {
      updatedFilters[key] = val;
    }
  });

  // 4️⃣ Remove keys that existed before but now missing from both sources
  Object.keys(oldFilters).forEach((key) => {
    const inEvent = Object.prototype.hasOwnProperty.call(tableFilters, key);
    const inAdv = Object.prototype.hasOwnProperty.call(advFilters, key);

    // Case: field not present in either filter payloads → remove it
    if (!inEvent && !inAdv) {
      console.log(`🗑️ Removing missing filter: ${key}`);
      delete updatedFilters[key];
    }

    // Case: field present but cleared (null, empty, etc.)
    else if (
      (inEvent && (tableFilters[key] === null || tableFilters[key] === '' || (Array.isArray(tableFilters[key]) && tableFilters[key].length === 0))) ||
      (inAdv && (advFilters[key] === null || advFilters[key] === '' || (Array.isArray(advFilters[key]) && advFilters[key].length === 0)))
    ) {
      console.log(`🗑️ Removing cleared filter: ${key}`);
      delete updatedFilters[key];
    }
  });
