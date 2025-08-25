// Utility: flatten tree into value → labelPath
function flattenOptions(options: any[], parentLabel: string = ''): Record<string, string> {
  let map: Record<string, string> = {};

  for (const opt of options) {
    const labelPath = parentLabel ? `${parentLabel} > ${opt.label}` : opt.label;
    map[opt.value] = labelPath;

    if (opt.items && opt.items.length > 0) {
      Object.assign(map, flattenOptions(opt.items, labelPath));
    }
  }

  return map;
}

// --- Inside your initForm ---
if (search.field === 'modelType') {
  const valueMap = flattenOptions(search.options);   // build dictionary

  const selectedLabels = (search.value || []).map((val: string) =>
    valueMap[val] || val   // fallback to raw if not found
  );

  console.log('Resolved labels for ModelType:', selectedLabels);

  this.searchFrom.addControl(
    search.field,
    new FormControl(search.value)   // keep raw values for API
  );

  // 👉 if dropdown needs both value + label (some libs do):
  // this.searchFrom.addControl(
  //   search.field,
  //   new FormControl(selectedLabels.map((label, i) => ({ value: search.value[i], label })))
  // );
}
// Utility: flatten tree into value → labelPath
function flattenOptions(options: any[], parentLabel: string = ''): Record<string, string> {
  let map: Record<string, string> = {};

  for (const opt of options) {
    const labelPath = parentLabel ? `${parentLabel} > ${opt.label}` : opt.label;
    map[opt.value] = labelPath;

    if (opt.items && opt.items.length > 0) {
      Object.assign(map, flattenOptions(opt.items, labelPath));
    }
  }

  return map;
}

// --- Inside your initForm ---
if (search.field === 'modelType') {
  const valueMap = flattenOptions(search.options);   // build dictionary

  const selectedLabels = (search.value || []).map((val: string) =>
    valueMap[val] || val   // fallback to raw if not found
  );

  console.log('Resolved labels for ModelType:', selectedLabels);

  this.searchFrom.addControl(
    search.field,
    new FormControl(search.value)   // keep raw values for API
  );

  // 👉 if dropdown needs both value + label (some libs do):
  // this.searchFrom.addControl(
  //   search.field,
  //   new FormControl(selectedLabels.map((label, i) => ({ value: search.value[i], label })))
  // );
}
