getTopLevelOptionLabel(options: any[], value: string): string | null {
  for (const opt of options) {
    if (opt.value === value) {
      return opt.label; // direct match
    }
    if (opt.items) {
      // check children
      const found = this.getTopLevelOptionLabel(opt.items, value);
      if (found) {
        return opt.label; // 👈 return parent instead of child
      }
    }
  }
  return null;
}


if (search.field === 'modelType') {
  const parentLabel = this.getTopLevelOptionLabel(search.options, search.value?.[0]);

  if (parentLabel) {
    this.searchFrom.addControl(
      search.field,
      new FormControl([search.value?.[0]])  // keep real value
    );

    console.log('Default label should be:', parentLabel);
  } else {
    this.searchFrom.addControl(search.field, new FormControl(search.value));
  }
}
