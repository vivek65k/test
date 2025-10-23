fetchData(event?: any, filters?: any): void {
  const prevFilters = this.filters || {};
  const tableFilters = event?.filterDto || {};

  // 🧠 If event exists → merge and search
  if (event) {
    const combined = { ...prevFilters, ...tableFilters };
    const updatedFilters: any = {};

    Object.entries(combined).forEach(([key, val]) => {
      if (val !== null && val !== undefined && val !== '' && (!Array.isArray(val) || val.length > 0)) {
        updatedFilters[key] = val;
      }
    });

    this.filters = updatedFilters;
  } 
  // 🧹 If no event (clear trigger) → remove cleared keys
  else {
    Object.entries(prevFilters).forEach(([key, val]) => {
      if (
        val === null ||
        val === undefined ||
        val === '' ||
        (Array.isArray(val) && val.length === 0)
      ) {
        delete prevFilters[key];
      }
    });

    this.filters = { ...prevFilters };
  }
