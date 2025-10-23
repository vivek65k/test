fetchData(event?: any, filters?: any): void {
  const prevFilters = { ...(this.filters || {}) };
  const tableFilters = event?.filterDto || {};
  const advFilters = filters?.filters || this.advFiltersList || {};
  this.advFiltersList = advFilters;

  // Step 1️⃣ - Merge both filter types
  const combined = { ...advFilters, ...tableFilters };
  const updatedFilters: any = {};

  // Step 2️⃣ - Keep valid (non-empty) filters only
  Object.entries(combined).forEach(([key, val]) => {
    if (val !== null && val !== undefined && val !== '' && (!Array.isArray(val) || val.length > 0)) {
      updatedFilters[key] = val;
    }
  });

  // Step 3️⃣ - Handle "clear" logic separately for table & advanced
  // (remove only cleared keys from respective filter sources)
  const isTableClear = event && Object.keys(tableFilters).length > 0;
  const isAdvClear = filters && Object.keys(filters?.filters || {}).length > 0;

  if (isTableClear) {
    Object.entries(tableFilters).forEach(([key, val]) => {
      if (
        val === null ||
        val === undefined ||
        val === '' ||
        (Array.isArray(val) && val.length === 0)
      ) {
        delete prevFilters[key]; // remove cleared table key only
      }
    });
  }

  if (isAdvClear) {
    Object.entries(filters.filters).forEach(([key, val]) => {
      if (
        val === null ||
        val === undefined ||
        val === '' ||
        (Array.isArray(val) && val.length === 0)
      ) {
        delete prevFilters[key]; // remove cleared advanced key only
        delete advFilters[key];
      }
    });
  }

  // Step 4️⃣ - Merge (old valid + new updates)
  const finalFilters = { ...prevFilters, ...updatedFilters };

  // Step 5️⃣ - Save and call API
  this.filters = { ...finalFilters };
  this.loaderService.show({ showMask: true });

  this.currentPage = event?.current || this.currentPage;
  this.defaultPageSize = event?.pageSize || this.defaultPageSize;

  const param = {
    current: this.currentPage,
    pageSize: this.defaultPageSize,
    sorts: this.sortOptions,
    filterDto: this.filters,
  };

  console.log('🧠 FINAL FILTERS =>', this.filters);


