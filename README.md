orgSelectedItems(event: any[]) {
  // keys of rows on current page
  const currentPageKeys = this.data.map(
    item => `${item.docId}-${item.modelId}-${item.wfInstanceId}`
  );

  // remove rows from this page (to avoid duplicates or stale)
  this.selectedItem = this.selectedItem.filter(
    item => !currentPageKeys.includes(
      `${item.docId}-${item.modelId}-${item.wfInstanceId}`
    )
  );

  // add back the rows that are actually selected on this page
  event.forEach(row => {
    const rowKey = `${row.docId}-${row.modelId}-${row.wfInstanceId}`;
    const exists = this.selectedItem.some(
      item => `${item.docId}-${item.modelId}-${item.wfInstanceId}` === rowKey
    );
    if (!exists) {
      this.selectedItem.push(row);
    }
  });

  console.log('Parent selectedItem:', this.selectedItem);
}
