// ✅ This will take options and return all child items in a flat array
flattenOptions(options: any[]): any[] {
  const flat: any[] = [];
  for (const opt of options) {
    if (opt.items && Array.isArray(opt.items)) {
      flat.push(...this.flattenOptions(opt.items)); // go deeper
    } else {
      flat.push(opt);
    }
  }
  return flat;
}



for (const search of this.searchItems) {
  if (search.field === 'modelType') {
    // Flatten all nested options
    const flatOptions = this.flattenOptions(search.options);

    // Find the matching option
    const selected = flatOptions.find(o => o.value === search.value[0]);

    // Add the form control with correct default
    if (selected) {
      this.searchFrom.addControl(
        search.field,
        new FormControl([selected.value]) // ✅ works with dropdown
      );
    } else {
      this.searchFrom.addControl(search.field, new FormControl(search.value));
    }
  } else {
    // Existing logic for other fields
    this.searchFrom.addControl(search.field, new FormControl(search.value));
  }
}
