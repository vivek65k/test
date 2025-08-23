function collectDeepestValues(models: any[]): string[] {
  const result: string[] = [];

  function traverse(model: any) {
    if (model.items && model.items.length > 0) {
      // go deeper for all children
      model.items.forEach((child: any) => traverse(child));
    } else {
      // leaf node (deepest)
      result.push(model.value);
    }
  }

  models.forEach(m => traverse(m));
  return result;
}
