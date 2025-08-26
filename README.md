static validSearchCriteria(min: number, criteriaName: 'ModelId' | 'WorkflowIds'): ValidatorFn {
   
    const regexResolver = (() => {
      const patterns: { [key: string]: () => RegExp } = {
        ModelId: () => new RegExp(/^M{2}([\s,]*\d+)+$/),
        WorkflowIds: () => new RegExp(/^[a-zA-Z]{1,2}\d+(,[a-zA-Z]{1,2}\d+)*$/)
      };
      return (key: string): RegExp =>
        (patterns[key] && typeof patterns[key] === 'function')
          ? patterns[key]() : /.*/; 
    })();

   
    return (control: AbstractControl): ValidationErrors | null => {
      const val: any = control?.value ?? '';
      const regex = regexResolver(criteriaName);


      const clean = (x: string) =>
        (x || '')
          .replace(/[\n\t,]/g, '')
          .trim();

      switch (true) {
        case !val || val.length === 0:
          return null;

        case val.length < min:
          return { [`invalid${criteriaName}Length`]: true };

        default:
          const transformed = clean(val);
          return regex.test(transformed)
            ? null
            : { [`invalid${criteriaName}Pattern`]: true };
      }
    };
  }
