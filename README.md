clearSearchFields() {
  this.advancedSearchGroupTool?.onClear();

  if (this.advancedSearchGroupTool) {
    this.advancedSearchGroupTool.executed = false;
  }

  this.filters = {};
  this.selectedItem = [];
  this.isSelectedAll = false;
  this.data = [];
  this.secondTableLoad = false;
  this.isFirstLoad = true;
  this.documentInventorytable?.reset();
  this.disableSearch = true;
  this.commonGridService.onClearFilters();

  // reset search form properly
  this.searchForm.reset();
  this.searchForm.markAsPristine();
  this.searchForm.markAsUntouched();
  this.searchForm.updateValueAndValidity();
}


get isSearchEnabled(): boolean {
  if (!this.searchForm.valid) return false;

  return Object.values(this.searchForm.value).some(value => {
    if (Array.isArray(value)) {
      return value.length > 0;
    }
    if (value === null || value === undefined) {
      return false;
    }
    return value.toString().trim().length > 0;
  });
}
