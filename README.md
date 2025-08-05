<ckeditor [editor]="Editor" [(ngModel)]="editorData"></ckeditor>




import * as ClassicEditor from '@ckeditor/ckeditor5-build-classic';

export class AppComponent {
  public Editor = ClassicEditor;
  public editorData = '<p>Hllo from CKEditor 5!</p>';
}

