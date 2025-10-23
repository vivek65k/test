Object.entries(updatedFilters).forEach(([key, value]) => {
  const isEventKey = event?.filterDto && Object.prototype.hasOwnProperty.call(event.filterDto, key);
  const isAdvKey = filters?.filters && Object.prototype.hasOwnProperty.call(filters.filters, key);

  // ✅ Keep only keys that exist in event or advanced filter
  if (isEventKey || isAdvKey) {
    // valid key — keep it
    updatedFilters[key] = value;
  } else {
    // key not part of current request — remove it
    delete updatedFilters[key];
  }
});
