private normalizeValue(value: any): string[] {
  if (Array.isArray(value)) {
    if (value.length > 0 && typeof value[0] === 'object' && 'value' in value[0]) {
      return value.flatMap((v: any) =>
        Array.isArray(v.value) ? v.value : [v.value]
      ).map(String);
    }
    return value.map(String);
  }
  return [String(value)];
}


const globalSearch: any = {};
Object.entries(globalFilter).forEach(([key, value]) => {
  globalFilter[key] = this.normalizeValue(value);
});
