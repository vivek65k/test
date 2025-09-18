<div *ngIf="
      col.badgeLabel &&
      (
        !col.pipeData?.badge?.whenField ||
        rowData[col.pipeData.badge.whenField] ===
          (col.pipeData.badge.whenEquals ?? true)
      )
    ">
  <mt-badge
    [label]="col.badgeLabel"
    [color]="
      (col.pipeData?.badge?.colorByValue?.[rowData[col.field]]) ||
      col.pipeData?.badge?.defaultColor || 'info'
    "
    class="lmn-ui-xs">
  </mt-badge>
</div>
