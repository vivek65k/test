private normalizeValue(value: any): string[] | null {
  if (value == null) {
    return null; 
  }
  if (Array.isArray(value)) {
    if (value.length === 0) {
      return null; 
    }   
    if (typeof value[0] === 'object' && value[0] && 'value' in value[0]) {
      return value.flatMap((v: any) =>
        Array.isArray(v.value) ? v.value : [v.value]
      )
      .filter(v => v != null && String(v).trim() !== '')
      .map(String);
    }   
    return value
      .filter(v => v != null && String(v).trim() !== '') 
      .map(String);
  } 
  const str = String(value).trim();
  return str ? [str] : null; 
}
