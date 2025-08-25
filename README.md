 if (nextFilter.type === this.gridColumnSearchType.Date) {
      const beforeKey = `${nextFilter.field}Before`
      const laterKey = `${nextFilter.field}LaterThan`

      nextFilter.value = [
        nextGroup.search[laterKey] || null,
        nextGroup.search[beforeKey] || null
      ].filter(Boolean)  // keep only non-null values

      // ✅ Patch into form controls too
      this.searchFrom.get(beforeKey)?.setValue(nextGroup.search[beforeKey])
      this.searchFrom.get(laterKey)?.setValue(nextGroup.search[laterKey])
    }
