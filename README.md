fetchData(event?: any, filters?: any) {
  // 1️⃣ Extract both sources
  const tableFilters = event?.filterDto || {};
  const advFilters = filters?.filters || {};
  const oldFilters = this.filters || {};

  // 2️⃣ Merge both incoming sources (table + advanced)
  const incoming = { ...advFilters, ...tableFilters };

  // 3️⃣ Initialize a clean new filter object
  const updatedFilters: any = {};

  // 4️⃣ Merge logic — add/update valid values
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

  // 5️⃣ Remove cleared or missing keys
  Object.keys(oldFilters).forEach((key) => {
    // If missing or empty in new filters, drop it
    if (
      !Object.prototype.hasOwnProperty.call(incoming, key) ||
      incoming[key] === null ||
      incoming[key] === undefined ||
      incoming[key] === '' ||
      (Array.isArray(incoming[key]) && incoming[key].length === 0)
    ) {
      console.log(`🗑️ Removing cleared filter: ${key}`);
      delete updatedFilters[key];
    }
  });

  // 6️⃣ Assign and refresh UI
  this.filters = updatedFilters;

  console.log('✅ Final Unified Filters:', this.filters);

  this.loaderService.show({ showMask: true });
  this.currentPage = event?.current || this.currentPage;
  this.defaultPageSize = event?.pageSize || this.defaultPageSize;
  this.sortOptions = event?.sorts || this.sortOptions;
}
