orgSelectedItems(event: any) {
  const currentPageKeys = this.data.map(
    item => `${item.docId}-${item.modelId}-${item.wfInstanceId}`
  );

  // 1. Remove deselected rows from current page
  this.selectedItem = this.selectedItem.filter(
    item => !currentPageKeys.includes(
      `${item.docId}-${item.modelId}-${item.wfInstanceId}`
    )
  );

  // 2. Add back the new selected rows from this page
  event.forEach((row: any) => {
    const rowKey = `${row.docId}-${row.modelId}-${row.wfInstanceId}`;
    const exists = this.selectedItem.some(
      item => `${item.docId}-${item.modelId}-${item.wfInstanceId}` === rowKey
    );
    if (!exists) {
      this.selectedItem.push(row);
    }
  });

  console.log('Final selectedItem:', this.selectedItem);
}
