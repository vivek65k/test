if (key === 'workflowCompletionDate') {
        // always save as [laterThan, before]
        const later = this.searchForm.get(`${key}LaterThan`)?.value || null;
        const before = this.searchForm.get(`${key}Before`)?.value || null;

        next.search[key] = [later, before];   // push both into array
