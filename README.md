Object.entries(updatedFilters).forEach(([key, value]) => {
  const eventFilters = event?.filterDto || {};
  const advFilters = filters?.filters || {};

  const isEventKey = Object.prototype.hasOwnProperty.call(eventFilters, key);
  const isAdvKey = Object.prototype.hasOwnProperty.call(advFilters, key);

  // 🧠 Case 1: filtering from TABLE only (filters undefined)
  if (event && !filters) {
    // Remove key only if it's from table and cleared
    if (isEventKey && (value === null || value === '' || (Array.isArray(value) && value.length === 0))) {
      console.log('🗑 Removing TABLE key:', key);
      delete updatedFilters[key];
    }
  }

  // 🧠 Case 2: filtering from ADVANCED only (event undefined)
  else if (!event && filters) {
    // Remove key only if it's from advanced and cleared
    if (isAdvKey && (value === null || value === '' || (Array.isArray(value) && value.length === 0))) {
      console.log('🗑 Removing ADV key:', key);
      delete updatedFilters[key];
    }
  }

  // 🧠 Case 3: both exist together (rare combined trigger)
  else if (event && filters) {
    // Remove only keys that are cleared in *both* sides
    if (
      (!isEventKey && !isAdvKey) ||
      (value === null || value === '' || (Array.isArray(value) && value.length === 0))
    ) {
      console.log('🗑 Removing COMMON key:', key);
      delete updatedFilters[key];
    }
  }
});
