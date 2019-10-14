# Component Styles

One way to do this is to set the `styles` property in the `component metadata`. The styles property **takes an array of strings that contain CSS code**. Usually you give it one string.

```ts
@Component({
  selector: 'app-root',
  template: `
    <h1>Tour of Heroes</h1>
    <app-hero-main [hero]="hero"></app-hero-main>
  `,
  styles: ['h1 { font-weight: normal; }']
})
export class HeroAppComponent {
/* . . . */
}
```

They are not inherited by any components nested within the template nor by any content projected into the component.