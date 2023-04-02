# wasm-example

### Компиляция & запуск

Команда для компиляции в wasm:

        wasm-pack build --target web --out-dir public/pkg
        

Для запуска я юзаю утилиту [serve](https://www.npmjs.com/package/serve):

        serve public/    
        
### wasm-bindgen
        
Ссылаемся на функцию [alert](https://developer.mozilla.org/ru/docs/Web/API/Window/alert) из js в rust'e:

        #[wasm_bindgen]
        extern {
            pub fn alert(s: &str);
        }

Экспортим фукнцию из rust в js:

        #[wasm_bindgen]
        pub fn greet(name: &str) {
            alert(&format!("Hello, {}!", name));
        }

Подробнее смотри: [src/lib.rs](https://github.com/artemkons/wasm-example/blob/main/src/lib.rs)
        
Использование экспортированной из rust функции greet в js:
        
        import init, { greet } from "./pkg/wasm_example.js";

        async function run() {
            await init();
            greet('artemkons')
        }

        run();


Подробнее смотри: [public/index.html](https://github.com/artemkons/wasm-example/blob/main/public/index.html)
