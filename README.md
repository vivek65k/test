flattenOptions(options: any[], parentLabel: string = ''): any[] {
  const flat: any[] = [];
  for (const opt of options || []) {
    if (opt.items && Array.isArray(opt.items)) {
      // Pass parent label down
      flat.push(...this.flattenOptions(opt.items, opt.label));
    } else {
      flat.push({
        label: parentLabel || opt.label,  // 👈 Always take top-level parent label
        value: opt.value
      });
    }
  }
  return flat;
}


if (search.field === 'modelType') {
  const flatOptions = this.flattenOptions(search.options || []);

  const selected = flatOptions.find(o => o.value === search.value?.[0]);

  if (selected) {
    this.searchFrom.addControl(
      search.field,
      new FormControl([selected.value])
    );
  } else {
    this.searchFrom.addControl(search.field, new FormControl(search.value));
  }
}
