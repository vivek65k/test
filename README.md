function normalizeFilterItems(items: any[]): any[] {
  const result: any[] = []

  items.forEach(item => {
    if (Array.isArray(item.value)) {
      // workflowStatus style
      item.value.forEach((val: string) => {
        result.push({ value: val, label: item.label })
      })
    } else {
      // vlName style
      result.push(item)
    }
  })

  return result
}
