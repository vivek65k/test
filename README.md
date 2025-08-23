function normalizeModelTypes(models: any[]): any[] {
  return models.map(model => {
    if (model.items && model.items.length > 0) {
      // recurse
      const normalizedChildren = normalizeModelTypes(model.items);

      // ✅ keep label & children, but replace parent value with *deepest child value*
      return {
        ...model,
        value: normalizedChildren[normalizedChildren.length - 1].value,
        items: normalizedChildren
      };
    }

    // leaf node – return as is
    return {
      label: model.label,
      value: model.value
    };
  });
}
