const prevFilters = this.filters || {};
  const tableFilters = event?.filterDto || {};
  const advFilters = filters?.filters || {};

  // Step 1️⃣ Combine both table & advanced filters
  const combined = { ...advFilters, ...tableFilters };

  // Step 2️⃣ Create new final object
  const updatedFilters: any = {};

  // Step 3️⃣ Merge & clean up valid values
  Object.entries(combined).forEach(([key, val]) => {
    if (
      val !== null &&
      val !== undefined &&
      val !== '' &&
      (!Array.isArray(val) || val.length > 0)
    ) {
      updatedFilters[key] = val;
    }
  });

  // Step 4️⃣ Keep previously active filters if they weren’t cleared or overridden
  Object.entries(prevFilters).forEach(([key, oldVal]) => {
    // If the new combined filters didn’t include this key (not cleared)
    // → keep it as is
    if (
      !Object.prototype.hasOwnProperty.call(combined, key) &&
      oldVal !== null &&
      oldVal !== undefined &&
      oldVal !== '' &&
      (!Array.isArray(oldVal) || oldVal.length > 0)
    ) {
      updatedFilters[key] = oldVal;
    }
  });

  // Step 5️⃣ Apply final cleaned filter set
  console.log("🧩 Final Filters:", updatedFilters);
