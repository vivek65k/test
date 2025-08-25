if (filterDto['workflowStatus'] && Array.isArray(filterDto['workflowStatus'])) {
  filterDto['workflowStatus'] = filterDto['workflowStatus'].map((v: any) =>
    Array.isArray(v) ? v : [v]  
  );
}
