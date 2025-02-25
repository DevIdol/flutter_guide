## Clean Architecture with Bloc + Cubit

- requirements and features တွေ အပေါ် မူတည်ပြီး folder structure ကို ပြောင်းနိုင်ပါတယ်

- Clean Architecture က large-scale apps အတွက် အကောင်းဆုံး ဖြစ်ပြီး၊ maintainability နဲ့ testability ကို အဓိ ထားထားပါတယ်။

```sh
lib/
├── config/                         # App-wide configurations
│   ├── app_config.dart             # App constants (e.g., app name, version)
│   ├── environment.dart            # Environment configs (dev, prod)
│   └── theme.dart                  # App theme (colors, typography)
├── core/                           # Core utilities
│   ├── error/                      # Error handling
│   │   ├── exceptions.dart         # Custom exceptions
│   │   └── failures.dart           # Failure classes (e.g., ServerFailure)
│   ├── network/                    # Network utilities
│   │   ├── dio_client.dart         # Dio setup with base URL
│   │   ├── interceptors.dart       # Dio interceptors (auth, logging)
│   │   └── network_info.dart       # Network connectivity check
│   └── usecases/                   # Base use case class
│       └── usecase.dart            # Abstract use case template
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
│   └── repositories/               # Repository implementations
│       ├── auth_repository_impl.dart # Auth repository
│       ├── product_repository_impl.dart # Product repository
│       ├── cart_repository_impl.dart # Cart repository
│       ├── payment_repository_impl.dart # Payment repository
│       └── order_repository_impl.dart # Order repository
├── domain/                         # Business logic layer
│   ├── entities/                   # Pure business entities
│   │   ├── user.dart               # User entity
│   │   ├── product.dart            # Product entity
│   │   ├── cart_item.dart          # Cart item entity
│   │   ├── order.dart              # Order entity
│   │   └── payment.dart            # Payment entity
│   ├── repositories/               # Abstract repository interfaces
│   │   ├── auth_repository.dart    # Auth interface
│   │   ├── product_repository.dart # Product interface
│   │   ├── cart_repository.dart    # Cart interface
│   │   ├── payment_repository.dart # Payment interface
│   │   └── order_repository.dart   # Order interface
│   └── usecases/                   # Business use cases
│       ├── auth/                   # Auth use cases
│       │   ├── login.dart          # Login use case
│       │   ├── signup.dart         # Signup use case
│       │   └── logout.dart         # Logout use case
│       ├── product/                # Product use cases
│       │   ├── get_products.dart   # Fetch products
│       │   └── get_product_details.dart # Fetch product details
│       ├── cart/                   # Cart use cases
│       │   ├── add_to_cart.dart    # Add to cart
│       │   └── remove_from_cart.dart # Remove from cart
│       ├── payment/                # Payment use cases
│       │   └── process_payment.dart # Process payment
│       └── order/                  # Order use cases
│           ├── place_order.dart    # Place order
│           └── get_order_history.dart # Fetch order history
├── presentation/                   # UI and state management
│   ├── routes/                     # Navigation with Go Router
│   │   ├── app_routes.dart         # Route definitions
│   │   └── router.dart             # Go Router setup
│   ├── screens/                    # Main app screens
│   │   ├── auth/                   # Authentication screens
│   │   │   ├── login_screen.dart   # Login UI with Cubit
│   │   │   └── signup_screen.dart  # Signup UI with Cubit
│   │   ├── home_screen.dart        # Home screen with Bloc
│   │   ├── product_detail_screen.dart # Product details UI
│   │   ├── cart_screen.dart        # Cart UI with Bloc
│   │   ├── payment_screen.dart     # Payment UI with Cubit
│   │   └── order_history_screen.dart # Order history UI
│   ├── widgets/                    # Reusable UI components
│   │   ├── product_card.dart       # Product item widget
│   │   ├── cart_item_widget.dart   # Cart item widget
│   │   ├── custom_button.dart      # Custom button widget
│   │   └── loading_indicator.dart  # Loading spinner
│   └── bloc/                       # Bloc and Cubit state management
│       ├── auth_cubit/             # Auth Cubit (simpler state)
│       │   ├── auth_cubit.dart     # Cubit
│       │   └── auth_state.dart     # State
│       ├── product_bloc/           # Product Bloc (complex state)
│       │   ├── product_bloc.dart   # Bloc
│       │   ├── product_event.dart  # Events
│       │   └── product_state.dart  # States
│       ├── cart_bloc/              # Cart Bloc
│       │   ├── cart_bloc.dart      # Bloc
│       │   ├── cart_event.dart     # Events
│       │   └── cart_state.dart     # States
│       ├── payment_cubit/          # Payment Cubit
│       │   ├── payment_cubit.dart  # Cubit
│       │   └── payment_state.dart  # State
│       └── order_bloc/             # Order Bloc
│           ├── order_bloc.dart     # Bloc
│           ├── order_event.dart    # Events
│           └── order_state.dart    # States
├── utils/                          # Helper utilities
│   ├── constants.dart              # Static constants (e.g., API endpoints)
│   ├── logger.dart                 # Logging utility
│   ├── validators.dart             # Input validation helpers
│   └── extensions.dart             # Dart extensions
├── services/                       # External services
│   ├── api_service.dart            # API service using Dio
│   ├── storage_service.dart        # Local storage (e.g., SharedPreferences, Hive)
│   └── payment_service.dart        # Payment gateway (e.g., Stripe, PayPal)
└── main.dart                       # App entry point with BlocProvider
```

### Clean Architecture with Bloc + Cubit Flowchart

```t
[Start: User Interaction]
       |
       v
[Presentation: PaymentScreen]
       | "User clicks 'Place Order'"
       v
[Bloc: OrderBloc]
       | "Receives PlaceOrderEvent"
       | "Calls PlaceOrder UseCase"
       v
[Domain: PlaceOrder UseCase]
       | "Defines business logic"
       | "Calls OrderRepository"
       v
[Data: OrderRepositoryImpl]
       | "Implements repository interface"
       | "Decides local or remote source"
       v
[Data: OrderLocalDataSource or OrderRemoteDataSource]
       | "Saves order locally or sends via DioClient"
       v
[Model: Order]
       | "Returns order data to Repository"
       v
[Data: OrderRepositoryImpl]
       | "Returns success/failure to UseCase"
       v
[Domain: PlaceOrder UseCase]
       | "Returns result to OrderBloc"
       v
[Bloc: OrderBloc]
       | "Emits OrderState (e.g., OrderPlaced)"
       v
[Presentation: PaymentScreen]
       | "Listens to OrderBloc state"
       | "Shows success or error UI"
       v
[End: User sees order confirmation]
```
