orgSelectedItems(event: any) {
  const newSelection = [...event];

  // Merge with old selection
  newSelection.forEach(item => {
    const itemKey = `${item.docId}-${item.modelId}-${item.wfInstanceId}`;
    const alreadyExists = this.selectedItem.some(selected => {
      const selectedKey = `${selected.docId}-${selected.modelId}-${selected.wfInstanceId}`;
      return selectedKey === itemKey;
    });

    if (!alreadyExists) {
      this.selectedItem.push(item);
    }
  });

  // Also remove deselected ones from current page
  const currentPageKeys = this.data.map(item =>
    `${item.docId}-${item.modelId}-${item.wfInstanceId}`
  );

  this.selectedItem = this.selectedItem.filter(selected => {
    const selectedKey = `${selected.docId}-${selected.modelId}-${selected.wfInstanceId}`;
    return (
      !currentPageKeys.includes(selectedKey) || // not on this page
      newSelection.some(item =>
        `${item.docId}-${item.modelId}-${item.wfInstanceId}` === selectedKey
      )
    );
  });

  console.log('Final selectedItem:', this.selectedItem);
}
