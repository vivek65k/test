let parentLabel: string | null = null;

if (search.options && search.value?.length) {
  parentLabel = this.getTopLevelOptionLabel(search.options as any[], search.value[0]);
}
