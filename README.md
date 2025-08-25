function normalizeToString(val: string | string[]): string {
  if (Array.isArray(val)) {
    return val.length > 0 ? val[0] : '';   // pick first element or empty
  }
  return val;
}


if (key.endsWith('LaterThan') || key.endsWith('Before')) {
  const baseKey = key.replace('Before', '').replace('LaterThan', '');

  if (!next.search[baseKey]) {
    next.search[baseKey] = [];
  }

  if (key.endsWith('LaterThan')) {
    next.search[baseKey][0] = normalizeToString(value);
  } else if (key.endsWith('Before')) {
    next.search[baseKey][1] = normalizeToString(value);
  }
} else {
  // fallback for normal fields
  next.search[key] = value;
}
