  if (key.endsWith('Before') || key.endsWith('LaterThan')) {
        const baseKey = key.replace('Before', '').replace('LaterThan', '');

        if (!next.search[baseKey]) {
          next.search[baseKey] = [];
        }

        if (key.endsWith('LaterThan')) {
          next.search[baseKey][0] = value;   // index 0 = later
        } else if (key.endsWith('Before')) {
          next.search[baseKey][1] = value;   // index 1 = before
        }
