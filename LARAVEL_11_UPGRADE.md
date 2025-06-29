# Laravel 11 Upgrade

## Changes Made

This pull request upgrades the movie-app from Laravel 10 to Laravel 11. The following changes have been made:

### Core Framework Changes

1. **Updated `composer.json`**:
   - Upgraded Laravel framework from `^10.10` to `^11.0`
   - Updated PHP requirement to `^8.2`
   - Updated dependencies to Laravel 11 compatible versions
   - Removed Laravel Sanctum (wasn't being used)
   - Updated testing dependencies

2. **Bootstrap Application Structure**:
   - Replaced the old `bootstrap/app.php` with the new Laravel 11 structure
   - Moved middleware configuration from `app/Http/Kernel.php` to `bootstrap/app.php`
   - Moved rate limiting configuration from `RouteServiceProvider` to `bootstrap/app.php`
   - Updated routing configuration

3. **Removed Deprecated Files**:
   - HTTP Kernel is no longer needed (middleware configured in bootstrap/app.php)
   - RouteServiceProvider is no longer needed (routing configured in bootstrap/app.php)
   - Removed RouteServiceProvider from service providers list in `config/app.php`

### What You Need to Do After Merging

1. **Run Composer Update**:
   ```bash
   composer update
   ```

2. **Clear Application Cache**:
   ```bash
   php artisan config:clear
   php artisan cache:clear
   php artisan route:clear
   php artisan view:clear
   ```

3. **Run Tests**:
   ```bash
   php artisan test
   ```

4. **Optional Cleanup**:
   - You can safely delete `app/Http/Kernel.php` after confirming everything works
   - You can safely delete `app/Providers/RouteServiceProvider.php` after confirming everything works

### New Features Available in Laravel 11

- Health check endpoint at `/up`
- Improved performance and streamlined structure
- Better developer experience with simplified configuration
- Updated underlying dependencies for better security and performance

### Breaking Changes

- PHP 8.2 is now required (was 8.1)
- Some middleware configuration has moved - if you had custom middleware configurations in the HTTP Kernel, verify they've been properly moved to `bootstrap/app.php`

### Configuration Notes

- The HOME constant from RouteServiceProvider (`/home`) is preserved in the rate limiting logic
- All existing middleware configurations have been preserved
- All route files continue to work as before
