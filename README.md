fetchData(event?: any, filters?: any): void {
  const prevFilters = { ...(this.filters || {}) };
  const tableFilters = event?.filterDto || {};
  const advFilters = filters?.filters || this.advFiltersList || {};
  this.advFiltersList = advFilters;

  // STEP 1️⃣ – detect which keys were cleared
  const clearedKeys: string[] = [];

  // Check for cleared table filters
  Object.entries(tableFilters).forEach(([key, val]) => {
    if (
      val === null ||
      val === undefined ||
      val === '' ||
      (Array.isArray(val) && val.length === 0)
    ) {
      clearedKeys.push(key);
    }
  });

  // Check for cleared advanced filters
  Object.entries(advFilters).forEach(([key, val]) => {
    if (
      val === null ||
      val === undefined ||
      val === '' ||
      (Array.isArray(val) && val.length === 0)
    ) {
      clearedKeys.push(key);
    }
  });

  // STEP 2️⃣ – combine new filters (table + adv)
  const combined = { ...advFilters, ...tableFilters };

  const updatedFilters: any = {};
  Object.entries(combined).forEach(([key, val]) => {
    if (val != null && val !== '' && (!Array.isArray(val) || val.length > 0)) {
      updatedFilters[key] = val;
    }
  });

  // STEP 3️⃣ – remove only cleared keys from previous filters
  clearedKeys.forEach((key) => {
    delete prevFilters[key];
  });

  // STEP 4️⃣ – merge everything
  const finalFilters = { ...prevFilters, ...updatedFilters };

  // STEP 5️⃣ – update and call API
  this.filters = { ...finalFilters };
  this.loaderService.show({ showMask: true });

  this.currentPage = event?.current || this.currentPage;
  this.defaultPageSize = event?.pageSize || this.defaultPageSize;

  const params = {
    current: this.currentPage,
    pageSize: this.defaultPageSize,
    sorts: this.sortOptions,
    filterDto: this.filters,
  };

  console.log('🧠 FINAL FILTERS:', this.filters);

