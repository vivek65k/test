
  let selectedOption: any = null;

  if (search.options && search.value?.length) {
    const rawValue = search.value[0];

    // 🔎 Find option by nested search
    const findOption = (options: any[], value: string): any => {
      for (const opt of options) {
        if (opt.value === value) return opt;
        if (opt.items) {
          const found = findOption(opt.items, value);
          if (found) return found;
        }
      }
      return null;
    };

    selectedOption = findOption(search.options, rawValue);
  }

  if (selectedOption) {
    // ✅ Store both value + label
    this.searchFrom.addControl(
      search.field,
      new FormControl([{ value: selectedOption.value, label: selectedOption.label }])
    );
  } else {
    // fallback if no match found
    this.searchFrom.addControl(search.field, new FormControl(search.value));
  }

  console.log('Default modelType set as:', selectedOption);

