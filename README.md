it('should call getApplicableSectionsForSelectedDocUsage on dropdown change', () => {

  const item = {
    documentUsage: null
  };

  const selectedValue = {
    label: 'GENERAL AGREEMENT',
    value: '123'
  };

  spyOn(component, 'getApplicableSectionsForSelectedDocUsage');

  component.getApplicableSectionsForSelectedDocUsage(selectedValue, item);

  expect(component.getApplicableSectionsForSelectedDocUsage)
    .toHaveBeenCalledWith(selectedValue, item);
});
