### Php Playwright Docker image

This docker image allows easy testing of php applications using the internal dev server and [Playwright](https://playwright.dev) e2e tests.


### Playwright Configuration (Laravel)

Possible Playwright Configuration:
```ts
const config: PlaywrightTestConfig = {
    /* ... */
    webServer: {
        command: "php artisan serve --port=80 > php-server.log", // Server output will be saved in php-server.log
        reuseExistingServer: !process.env.CI,
        port: 80,
    },
    /* ... */
};
```

If you are using gitlab there is an example pipeline available to get you up and running:

[Gitlab Pipeline example](gitlab/laravel-example.gitlab-ci.yml)

### Playwright Configuration (Stock Php)

Possible Playwright Configuration:
```ts
const config: PlaywrightTestConfig = {
    /* ... */
    webServer: {
        command: "php -S localhost:80 > php-server.log", // Server output will be saved in php-server.log
        reuseExistingServer: !process.env.CI,
        port: 80,
    },
    /* ... */
};
```