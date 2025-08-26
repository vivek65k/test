static validSearchCriteria(min: number, criteriaName: 'ModelId' | 'WorkflowIds'): ValidatorFn {
  return (control: AbstractControl): ValidationErrors | null => {
    const v = (control?.value ?? '').toString();
    return !v
      ? null
      : v.length < min
        ? { [`invalid${criteriaName}Length`]: true }
        : new RegExp(
            criteriaName === 'ModelId'
              ? '^M{2}([\\s,]*\\d+)+$'
              : '^[a-zA-Z]{1,2}\\d+(,[a-zA-Z]{1,2}\\d+)*$'
          ).test(
            v.replace(/[\n\t,]/g, '').trim()
          )
          ? null
          : { [`invalid${criteriaName}Pattern`]: true };
  };
}
