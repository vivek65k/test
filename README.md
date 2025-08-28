 let beforeVal = '';
  let laterVal = '';
 if (controlvalue && typeof controlvalue === 'object' && !Array.isArray(controlvalue)) {
    beforeVal = controlvalue.before || '';
    laterVal = controlvalue.laterThan || '';
  }

   this.searchForm.addControl(`${search.field}Before`, new FormControl(beforeVal));
  this.searchForm.addControl(`${search.field}LaterThan`, new FormControl(laterVal));
