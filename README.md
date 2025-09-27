private buildFilterDto(): any {
  let filterDto: { [key: string]: string | string[] } = {};

  // workflowStatus
  if (this.filters['workFlowStatus']) {
    filterDto['workFlowStatus'] = (this.filters['workFlowStatus'] as string[])
      .flat()
      .map((item: string | string[]) => (Array.isArray(item) ? item[0] : item));
  }

  // workflowType
  if (this.filters['workFlowType']) {
    filterDto['workFlowType'] = (this.filters['workFlowType'] as string[])
      .flat()
      .map((item: string | string[]) => (Array.isArray(item) ? item[0] : item));
  }

  // normal filters
  Object.entries(this.filters).forEach(([key, value]) => {
    if (key !== 'workFlowStatus' && key !== 'workFlowType' && value?.length) {
      filterDto[key] = value;
    }
  });

  // ✅ merge with advanceSearchParams
  filterDto = this.mergeFilters(filterDto, this.advanceSearchParams?.search ?? {});

  return filterDto;
}
