## MVVM with Riverpod (Flutter Hooks + Hooks Riverpod) + Repository Folder Structure

- requirements and features တွေ အပေါ် မူတည်ပြီး folder structure ကို ပြောင်းနိုင်ပါတယ်

- MVVM က scalability နဲ့ data layer separation လိုတဲ့ medium-sized apps အတွက် အကောင်းဆုံး ဖြစ်ပါတယ်။

```sh
lib/
├── config/                         # App-wide configurations
│   ├── app_config.dart             # App constants (e.g., app name, version)
│   ├── environment.dart            # Environment configs (dev, prod)
│   └── theme.dart                  # App theme (colors, typography)
├── data/                           # Data layer
│   ├── datasources/                # Local and remote data sources
│   │   ├── local/                  # Local storage
│   │   │   ├── auth_local_datasource.dart # Local auth storage
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
│   ├── repositories/               # Repository implementations
│   │   ├── auth_repository.dart    # Auth data operations
│   │   ├── product_repository.dart # Product data operations
│   │   ├── cart_repository.dart    # Cart data operations
│   │   ├── payment_repository.dart # Payment data operations
│   │   └── order_repository.dart   # Order data operations
│   └── network/                    # Network utilities
│       ├── dio_client.dart         # Dio setup with base URL
│       └── interceptors.dart       # Dio interceptors (e.g., auth token, logging)
├── providers/                      # Riverpod providers
│   ├── auth_provider.dart          # Auth state provider
│   ├── product_provider.dart       # Product state provider
│   ├── cart_provider.dart          # Cart state provider
│   ├── payment_provider.dart       # Payment state provider
│   ├── order_provider.dart         # Order state provider
│   └── repository_provider.dart    # Repository dependency injection
├── routes/                         # Navigation with Go Router
│   ├── app_routes.dart             # Defines routes (e.g., /home, /cart)
│   └── router.dart                 # Go Router setup
├── utils/                          # Helper utilities
│   ├── constants.dart              # Static constants (e.g., API endpoints)
│   ├── logger.dart                 # Logging utility
│   ├── validators.dart             # Input validation helpers
│   └── extensions.dart             # Dart extensions
├── ui/                             # Presentation layer
│   ├── screens/                    # Main app screens
│   │   ├── auth/                   # Authentication screens
│   │   │   ├── login_screen.dart   # Login UI with hooks
│   │   │   └── signup_screen.dart  # Signup UI with hooks
│   │   ├── home_screen.dart        # Home screen with product listing
│   │   ├── product_detail_screen.dart # Product details UI
│   │   ├── cart_screen.dart        # Cart UI
│   │   ├── payment_screen.dart     # Payment checkout UI
│   │   └── order_history_screen.dart # Order history UI
│   ├── view_models/                # View models with Riverpod
│   │   ├── auth_view_model.dart    # Auth logic with providers
│   │   ├── product_view_model.dart # Product logic with providers
│   │   ├── cart_view_model.dart    # Cart logic with providers
│   │   ├── payment_view_model.dart # Payment logic with providers
│   │   └── order_view_model.dart   # Order logic with providers
│   └── widgets/                    # Reusable UI components
│       ├── product_card.dart       # Product item widget
│       ├── cart_item_widget.dart   # Cart item widget
│       ├── custom_button.dart      # Custom button widget
│       └── loading_indicator.dart  # Loading spinner
├── services/                       # External services
│   ├── api_service.dart            # API service using Dio
│   ├── storage_service.dart        # Local storage (e.g., SharedPreferences, Hive)
│   └── payment_service.dart        # Payment gateway (e.g., Stripe, PayPal)
└── main.dart                       # App entry point with ProviderScope
```

### MVVM with Riverpod Flowchart

```t
[Start: User Interaction]
       |
       v
[View: ProductDetailScreen]
       | "User navigates to product details"
       v
[ViewModel: ProductViewModel]
       | "Reads Riverpod ProductProvider"
       | "Triggers fetchProductDetails()"
       v
[Provider: ProductProvider]
       | "Manages state (loading, success, error)"
       | "Calls ProductRepository"
       v
[Repository: ProductRepository]
       | "Decides local or remote source"
       v
[Data: ProductLocalDataSource or ProductRemoteDataSource]
       | "Fetches data (local or via DioClient)"
       v
[Model: Product]
       | "Returns product data to Repository"
       v
[Repository: ProductRepository]
       | "Passes data to ProductProvider"
       v
[Provider: ProductProvider]
       | "Updates state with product data"
       v
[ViewModel: ProductViewModel]
       | "Listens to Provider state changes"
       v
[View: ProductDetailScreen]
       | "UI updates with product details"
       v
[End: User sees product details]
```
