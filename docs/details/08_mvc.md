## MVC with GetX State Management Folder Structure

- requirements and features တွေ အပေါ် မူတည်ပြီး folder structure ကို ပြောင်းနိုင်ပါတယ်

- MVC က ရိုးရှင်းပြီး small to medium-sized apps အတွက် အကောင်းဆုံး ရွေးချယ်မှုတစ်ခုပါ။

```sh
lib/
├── config/                         # App-wide configurations
│   ├── app_config.dart             # App constants (e.g., app name, version)
│   ├── environment.dart            # Environment configs (dev, prod)
│   └── theme.dart                  # App theme (colors, typography)
├── controllers/                    # GetX controllers for business logic
│   ├── auth_controller.dart        # Manages login, signup, logout
│   ├── cart_controller.dart        # Controls cart operations
│   ├── product_controller.dart     # Manages product listing/details
│   ├── payment_controller.dart     # Handles payment processing
│   └── order_controller.dart       # Manages order placement/history
├── data/                           # Data layer
│   ├── datasources/                # Local and remote data sources
│   │   ├── local/                  # Local storage (e.g., Hive, SharedPreferences)
│   │   │   ├── auth_local_datasource.dart # Stores auth tokens locally
│   │   │   ├── cart_local_datasource.dart # Local cart data
│   │   │   └── order_local_datasource.dart # Local order history
│   │   └── remote/                 # API data sources
│   │       ├── auth_remote_datasource.dart # Auth API calls
│   │       ├── product_remote_datasource.dart # Product API calls
│   │       ├── payment_remote_datasource.dart # Payment API calls
│   │       └── order_remote_datasource.dart # Order API calls
│   ├── models/                     # Data models (e.g., using freezed)
│   │   ├── user.dart               # User model
│   │   ├── product.dart            # Product model
│   │   ├── cart_item.dart          # Cart item model
│   │   ├── order.dart              # Order model
│   │   └── payment.dart            # Payment model
│   └── network/                    # Network utilities
│       ├── dio_client.dart         # Dio setup with base URL
│       └── interceptors.dart       # Dio interceptors (e.g., auth token, logging)
├── routes/                         # Navigation with GetX
│   ├── app_pages.dart              # Defines routes and bindings
│   └── app_routes.dart             # Route names (e.g., /home, /cart)
├── utils/                          # Helper utilities
│   ├── constants.dart              # Static constants (e.g., API endpoints)
│   ├── logger.dart                 # Logging utility
│   ├── validators.dart             # Input validation helpers
│   └── extensions.dart             # Dart extensions (e.g., String utils)
├── views/                          # UI screens and widgets
│   ├── screens/                    # Main app screens
│   │   ├── auth/                   # Authentication screens
│   │   │   ├── login_screen.dart   # Login UI
│   │   │   └── signup_screen.dart  # Signup UI
│   │   ├── home_screen.dart        # Home screen with product listing
│   │   ├── product_detail_screen.dart # Product details UI
│   │   ├── cart_screen.dart        # Cart UI
│   │   ├── payment_screen.dart     # Payment checkout UI
│   │   └── order_history_screen.dart # Order history UI
│   └── widgets/                    # Reusable UI components
│       ├── product_card.dart       # Product item widget
│       ├── cart_item_widget.dart   # Cart item widget
│       ├── custom_button.dart      # Custom button widget
│       └── loading_indicator.dart  # Loading spinner
├── services/                       # External services
│   ├── api_service.dart            # API service using Dio
│   ├── storage_service.dart        # Local storage (e.g., SharedPreferences, Hive)
│   └── payment_service.dart        # Payment gateway (e.g., Stripe, PayPal)
└── main.dart                       # App entry point with GetX initialization
```

### MVC with GetX Flowchart

```t
[Start: User Interaction]
       |
       v
[View: Cart Screen]
       | "User clicks 'Add to Cart'"
       v
[Controller: CartController]
       | "Handles business logic"
       | "Calls API or local storage via Data layer"
       v
[Data: CartLocalDataSource or CartRemoteDataSource]
       | "Fetches or updates cart data"
       | "Uses DioClient with Interceptors for API"
       v
[Model: CartItem]
       | "Updates cart state in CartController"
       v
[Controller: CartController]
       | "Notifies View via GetX reactive state"
       v
[View: Cart Screen]
       | "UI updates with new cart data"
       v
[End: User sees updated cart]
```
