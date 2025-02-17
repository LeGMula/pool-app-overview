# Pool Music App

[![Instagram](https://img.shields.io/badge/Instagram-%23E4405F.svg?style=for-the-badge&logo=Instagram&logoColor=white)](https://www.instagram.com/poolmusic.app/) 
[![App Store](https://img.shields.io/badge/App_Store-0D96F6?style=for-the-badge&logo=app-store&logoColor=white)](https://apps.apple.com/de/app/pool-music/id1589212656?l=en-GB) 
[![Google Play](https://img.shields.io/badge/Google_Play-414141?style=for-the-badge&logo=google-play&logoColor=white)](https://play.google.com/store/apps/details?id=app.poolmusic)

![image](https://github.com/user-attachments/assets/a0bc7960-b371-4b6e-a538-3c1b05af992b)



## System Architecture

### 1. Mobile Application (Flutter)

- **Framework**: Flutter SDK ^3.7.0
- **State Management**: Utilizes `flutter_bloc` and `hydrated_bloc` for efficient state handling
- **Key Features**: 
  - Real-time stock chart price & percentage change display
  - User authentication and verification
  - Dynamic updates for market data
- **Notable Dependencies**:
  - `flutter_bloc` for state management
  - `go_router` for navigation

#### Unique Solution: Error Handling

Our mobile app implements a sophisticated error handling mechanism using `flutter_bloc`:

```dart
class ErrorListener {
  void listener(BuildContext context, ErrorHandlerState state) {
    // Error handling logic
    if (state is TimeoutErrorState) {
      errorSnackBar = AppSnackBar(message: 'Server connection timeout. Please try again.');
    } else if (state is ValidationErrorState) {
      errorSnackBar = AppSnackBar(message: 'Server has returned an error. Please verify all information you have entered.');
    }
    // ... more error states ...
    
    if (errorSnackBar != null && showSnackBar) {
      ScaffoldMessenger.of(context).showSnackBar(errorSnackBar);
    }
  }
}

2. Web Admin Portal (Angular)

- **Framework**: Angular 16.0.5
- **Key Libraries**:
  - @angular/platform-browser
  - @angular/router
  - @angular/common
  - @angular/core
- **Main Functionalities**: 
  - User authentication
  - Statistics display
  - Verification processes
- **State Management**: Utilizes built-in Angular services for state management

3. Backend Services (Python)

- **Framework**: Django
- **Database**: PostgreSQL, chosen for its robustness and support for advanced features
- **Key Services**:
  - Profile management
  - Wallet operations
  - User verification
  - Market order processing

#### Complex API Endpoint Example: Wallet Withdrawal

```python
@method_decorator(name='post', decorator=doc_decorator)
class WalletWithdrawView(APIView):
    permission_classes = (FanOnly, HasWallet, IsVerified)

    def post(self, request):
        serializer = WalletWithdrawSerializer(
            data=request.data, context={'user': request.user}
        )
        serializer.is_valid(raise_exception=True)

        withdrawal_service = OPPWithdrawalService()
        withdrawal_service.create(
            user=request.user,
            amount=serializer.data['amount'],
        )

        return Response()
