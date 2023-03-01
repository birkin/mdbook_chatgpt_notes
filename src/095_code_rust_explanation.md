# Code - rust explanation

prompt...

```
explain this code...

fn main() {
    // Confirm current working directory
    let cwd = env::current_dir();
    println!("The current directory is {}", cwd.unwrap().display());

    // Load the image file
    let filepath = "./src/source_image/happy_ferris.png".to_string();
    let image_obj: image::DynamicImage = image::open(filepath).unwrap();

    // Convert the image to a base64-encoded string
    let mut image_data: Vec<u8> = Vec::new();
    image_obj
        .write_to(&mut Cursor::new(&mut image_data), ImageOutputFormat::Png)
        .unwrap();
    let res_base64 = base64::encode(image_data);
    print!("base64 output, ``{}``", res_base64)
}
```

- [link](http://localhost:3000/ex_code_rust_explanation.html)