# rushdown-icons

This is an extension for the [rushdown](https://crates.io/crates/rushdown) crate.

Draw named icons in a markdown document as inline SVG. A name written between double colons, such as `::lucide:zap::`, becomes an inline `<svg>`, so the page ships only the icons it uses.

The namespace comes first, and is mandatory. Four sets are available: Lucide, Octicons, Simple Icons and, behind the `fontawesome` feature, Font Awesome Free. The icon takes the size and the colour of the text around it, so prose needs no stylesheet.

Font Awesome Free icons sit under the CC BY 4.0 licence, so a page which renders one owes attribution. The licence terms and the note about the changes this crate makes are in [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).

## Usage

Add the crate via `cargo add rushdown-icons` and include it within your rushdown parser.

```rust
use rushdown::{new_markdown_to_html_string, parser::Options, renderer::html};
use rushdown_icons::{
    IconsHtmlRendererOptions, icons_html_renderer_extension, icons_parser_extension,
};

let convert = new_markdown_to_html_string(
    Options::default(),
    html::Options::default(),
    icons_parser_extension(),
    icons_html_renderer_extension::<String>(IconsHtmlRendererOptions::default()),
);
let mut out = String::new();
convert(&mut out, "Press ::lucide:zap:: to deploy.").unwrap();
assert!(out.contains(r#"class="icon icon-lucide-zap""#));
```
