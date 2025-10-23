Object.entries(updatedFilters).forEach(([key, value]) => {
  const eventFilters = event?.filterDto || {};
  const advFilters = filters?.filters || {};

  const isEventKey = Object.prototype.hasOwnProperty.call(eventFilters, key);
  const isAdvKey = Object.prototype.hasOwnProperty.call(advFilters, key);

  console.log('isEventKey', isEventKey, 'isAdvKey', isAdvKey, 'key', key, 'value', value);

  // ✅ remove key only if it doesn't exist in either source
  if (!isEventKey && !isAdvKey) {
    console.log('🗑 Removing key:', key);
    delete updatedFilters[key];
  }
});
