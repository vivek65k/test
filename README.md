fetchData(event?: any, filters?: any) {
  const prevFilters = this.filters || {};
  const newFilters = {
    ...(filters?.filters || {}),
    ...(event?.filterDto || {}),
  };

  const updateFilter: any = {};

  // Step 1: Add or update valid filters
  Object.entries(newFilters).forEach(([key, val]) => {
    if (
      val !== null &&
      val !== undefined &&
      val !== '' &&
      (!Array.isArray(val) || val.length > 0)
    ) {
      updateFilter[key] = val;
    }
  });

  // Step 2: Remove keys that were in old filters but not in new ones
  Object.keys(prevFilters).forEach((key) => {
    if (!Object.prototype.hasOwnProperty.call(newFilters, key)) {
      console.log(`🗑️ Clearing key because it's missing in new filters: ${key}`);
      // skip adding it → effectively deletes it
    } else if (
      newFilters[key] === null ||
      newFilters[key] === undefined ||
      newFilters[key] === '' ||
      (Array.isArray(newFilters[key]) && newFilters[key].length === 0)
    ) {
      console.log(`🗑️ Clearing key because new value is empty: ${key}`);
      // skip adding it → effectively deletes it
    } else {
      updateFilter[key] = newFilters[key];
    }
  });

  console.log('✅ Final updateFilter:', updateFilter);

  this.loaderService.show({ showMask: true });
  this.filters = updateFilter;
  this.currentPage = event?.current || this.currentPage;
  this.defaultPageSize = event?.pageSize || this.defaultPageSize;
  this.sortOptions = event?.sorts || this.sortOptions;
}
