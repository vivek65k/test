<ckeditor [editor]="Editor" [formControl]="editorControl"></ckeditor>



import { Component } from '@angular/core';
import { FormControl } from '@angular/forms';
import * as ClassicEditor from '@ckeditor/ckeditor5-build-classic';

@Component({
  selector: 'app-root',
  standalone: true,
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  public Editor = ClassicEditor;
  public editorControl = new FormControl('<p>Hello from CKEditor 5!</p>');
}


import { ReactiveFormsModule } from '@angular/forms';

bootstrapApplication(AppComponent, {
  providers: [
    provideAnimations(),
    importProvidersFrom(CKEditorModule, RouterModule, ReactiveFormsModule)
  ]
});


