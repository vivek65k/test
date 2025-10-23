fetchData(event?: any, filters?: any): void {
  const prevFilters = { ...(this.filters || {}) };
  const tableFilters = event?.filterDto || {};
  const advFilters = this.advFiltersList || filters?.filters || {};

  // STEP 1️⃣ - Detect cleared keys (empty or null)
  const clearedKeys: string[] = [];

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

  // STEP 2️⃣ - Remove cleared keys from previous state
  clearedKeys.forEach((key) => {
    delete prevFilters[key];
    delete advFilters[key];
  });

  // STEP 3️⃣ - Prepare valid table filters
  const updatedTableFilters: any = {};
  Object.entries(tableFilters).forEach(([key, val]) => {
    if (val != null && val !== '' && (!Array.isArray(val) || val.length > 0)) {
      updatedTableFilters[key] = val;
    }
  });

  // STEP 4️⃣ - Prepare valid advanced filters
  const updatedAdvFilters: any = {};
  Object.entries(advFilters).forEach(([key, val]) => {
    if (val != null && val !== '' && (!Array.isArray(val) || val.length > 0)) {
      updatedAdvFilters[key] = val;
    }
  });

  // STEP 5️⃣ - Merge all (priority: old + adv + table)
  const mergedFilters = { ...prevFilters, ...updatedAdvFilters, ...updatedTableFilters };

  // STEP 6️⃣ - Update references
  this.filters = mergedFilters;
  this.advFiltersList = updatedAdvFilters;

  // STEP 7️⃣ - Logging (optional)
  console.log("✅ Final Filters:", this.filters);
  console.log("✅ Adv Filters:", this.advFiltersList);
  console.log("✅ Table Filters:", updatedTableFilters);
  console.log("✅ Cleared Keys:", clearedKeys);
