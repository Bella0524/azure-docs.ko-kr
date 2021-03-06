---
title: "Xamarin.Forms 앱에서 Mobile Apps에 대한 인증 시작 | Microsoft Docs"
description: "모바일 앱을 사용하여 AAD, Google, Facebook, Twitter, Microsoft 등의 다양한 ID 공급자를 통해 Xamarin Forms 앱 사용자를 인증하는 방법을 알아봅니다."
services: app-service\mobile
documentationcenter: xamarin
author: adrianhall
manager: dwrede
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: adrianha
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 65c8ff42c9c34eb51cb26153eff9b45aa0926838


---
# <a name="add-authentication-to-your-xamarin-forms-app"></a>Xamarin Forms 앱에 인증 추가
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>개요
이 항목에서는 클라이언트 응용 프로그램에서 앱 서비스 모바일 앱의 사용자를 인증하는 방법을 보여 줍니다. 이 자습서에서는 App Service가 지원하는 ID 공급자를 사용하여 Xamarin.Forms 빠른 시작 프로젝트에 인증을 추가합니다. 모바일 앱에서 인증이 완료되고 권한이 부여되고 나면 사용자 ID 값이 표시되고 제한된 테이블 데이터에 액세스할 수 있게 됩니다.

## <a name="prerequisites"></a>필수 조건
이 자습서를 통한 최상의 결과를 얻기 위해 먼저 [Xamarin.Forms 앱 만들기][1] 자습서를 완료하는 것이 좋습니다. 이 자습서를 완료하면 다중 플랫폼 TodoList 앱인 Xamarin.Forms 프로젝트가 생깁니다.

다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 프로젝트에 인증 확장 패키지를 추가해야 합니다. 서버 확장 패키지에 대한 자세한 내용은 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용][2]을 참조하세요.

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>인증을 위해 앱 등록 및 앱 서비스 구성
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="restrict-permissions-to-authenticated-users"></a>사용 권한을 인증된 사용자로 제한
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a>이식 가능한 클래스 라이브러리에 인증 추가
Mobile Apps는 [MobileServiceClient][4]에서 [LoginAsync][3] 확장 메서드를 사용하여 App Service 인증으로 사용자를 로그인합니다. 이 샘플에서는 서버 관리 인증 흐름을 사용하여 앱에서 공급자의 로그인 인터페이스를 표시합니다. 자세한 내용은 [서버 관리 인증][5]을 참조하세요. 프로덕션 앱에서 향상된 사용자 환경을 제공하기 위해 대신 [클라이언트 관리 인증][6]을 사용하는 것을 고려할 수 있습니다.

Xamarin Forms 프로젝트를 사용하여 인증하기 위해서 앱에 대한 이식 가능한 클래스 라이브러리에 **IAuthenticate** 인터페이스를 정의합니다. 또한 이식 가능한 클래스 라이브러리에 정의된 사용자 인터페이스를 업데이트하여 **로그인** 단추를 추가합니다. 사용자는 이 단추를 클릭하여 인증을 시작합니다. 인증에 성공하면 Mobile App 백 엔드에서 데이터가 로드됩니다.

앱에서 지원되는 각 플랫폼에 대해 **IAuthenticate** 인터페이스를 구현합니다.

1. Visual Studio 또는 Xamarin Studio에서 이름에 **이식 가능**이 있는 프로젝트(이식 가능한 클래스 라이브러리 프로젝트)에서 App.cs를 연 후 다음 `using` 문을 추가합니다.
   
        using System.Threading.Tasks;
2. App.cs에 `App` 클래스 정의 직전에 다음과 같은 `IAuthenticate` 인터페이스 정의를 추가합니다.
   
        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. 플랫폼 전용 구현으로 인터페이스를 초기화하도록 **App** 클래스에 다음 정적 멤버를 추가합니다.
   
        public static IAuthenticate Authenticator { get; private set; }
   
        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. 이식 가능한 클래스 라이브러리 프로젝트에서 TodoList.xaml을 열고 **buttonsPanel** 레이아웃 요소의 다음 *Button* 요소를 기존 단추 뒤에 추가합니다.
   
          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>
   
    이 단추는 모바일 앱 백 엔드로 서버 관리 인증을 트리거합니다.
5. 이식 가능한 클래스 라이브러리 프로젝트에서 TodoList.xaml.cs를 연 후 다음 필드를 `TodoList` 클래스에 추가합니다.
   
        // Track whether the user has authenticated.
        bool authenticated = false;
6. **OnAppearing** 메서드를 다음 코드로 바꿉니다.
   
        protected override async void OnAppearing()
        {
            base.OnAppearing();
   
            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems to true in order to synchronize the data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);
   
                // Hide the Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }
   
    이렇게 코드를 변경하면 사용자가 인증된 후에만 데이터가 새로 고침됩니다.
7. **TodoList** 클래스에 **Clicked** 이벤트에 대한 다음 처리기를 추가합니다.
   
        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();
   
            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. 변경 내용을 저장하고 이식 가능한 클래스 라이브러리 프로젝트를 다시 빌드하여 오류가 없는지 확인합니다.

## <a name="add-authentication-to-the-android-app"></a>Android 앱에 인증 추가
이 섹션에는 Android 앱 프로젝트에서 **IAuthenticate** 인터페이스를 구현하는 방법을 보여 줍니다. Android 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.

1. Visual Studio 또는 Xamarin Studio에서 **droid** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 클릭합니다.
2. F5 키를 눌러 디버거에서 프로젝트를 실행하고 앱이 시작된 후 상태 코드 401(인증되지 않음)의 처리되지 않은 예외가 발생하는지 확인합니다. 백 엔드에서 액세스를 인증된 사용자만으로 제한했기 때문에 401 코드가 생성됩니다.
3. Android 프로젝트에서 MainActivity.cs를 열고 다음 `using` 문을 추가합니다.
   
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. 다음과 같이 **IAuthenticate** 인터페이스를 구현하도록 **MainActivity** 클래스를 업데이트합니다.
   
        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. 다음과 같이 **IAuthenticate** 인터페이스에 필요한 **MobileServiceUser** 필드 및 **Authenticate** 메서드를 추가하여 **MainActivity** 클래스를 업데이트합니다.
   
        // Define a authenticated user.
        private MobileServiceUser user;
   
        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this,
                    MobileServiceAuthenticationProvider.Facebook);
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }
   
            // Display the success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();
   
            return success;
        }

    Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider][7]에 대해 다른 값을 선택합니다.

1. `LoadApplication()`에 대한 호출 이전에 **MainActivity** 클래스의 **OnCreate** 메서드에 다음 코드를 추가합니다.
   
        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);
   
    이 코드를 사용하면 앱이 로드되기 전에 인증자가 초기화됩니다.
2. 앱을 다시 빌드하고 실행한 후 선택한 인증 공급자를 사용하여 로그인하고 인증된 사용자로 데이터에 액세스할 수 있는지 확인합니다.

## <a name="add-authentication-to-the-ios-app"></a>iOS 앱에 인증 추가
이 섹션에는 iOS 앱 프로젝트에서 **IAuthenticate** 인터페이스를 구현하는 방법을 보여 줍니다. iOS 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.

1. Visual Studio 또는 Xamarin Studio에서 **iOS** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 클릭합니다.
2. F5 키를 눌러 디버거에서 프로젝트를 실행하고 앱이 시작된 후 상태 코드 401(인증되지 않음)의 처리되지 않은 예외가 발생하는지 확인합니다. 백 엔드에서 액세스를 인증된 사용자만으로 제한했기 때문에 401 응답이 생성됩니다.
3. iOS 프로젝트에서 AppDelegate.cs를 열고 다음 `using` 문을 추가합니다.
   
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. 다음과 같이 **IAuthenticate** 인터페이스를 구현하도록 **AppDelegate** 클래스를 업데이트합니다.
   
        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. 다음과 같이 **IAuthenticate** 인터페이스에 필요한 **MobileServiceUser** 필드 및 **Authenticate** 메서드를 추가하여 **AppDelegate** 클래스를 업데이트합니다.
   
        // Define a authenticated user.
        private MobileServiceUser user;
   
        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook);
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }
   
            // Display the success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();
   
            return success;
        }
   
    Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider]에 대해 다른 값을 선택합니다.
6. `LoadApplication()`에 대한 호출 이전에 **FinishedLaunching** 메서드에 다음 코드 줄을 추가합니다.
   
        App.Init(this);
   
    이 코드를 사용하면 앱이 로드되기 전에 인증자가 초기화됩니다.
7. 앱을 다시 빌드하고 실행한 후 선택한 인증 공급자를 사용하여 로그인하고 인증된 사용자로 데이터에 액세스할 수 있는지 확인합니다.

## <a name="add-authentication-to-windows-81-including-phone-app-projects"></a>Windows 8.1(Phone 포함) 앱 프로젝트에 인증 추가
이 섹션에는 Windows 8.1 및 Windows Phone 8.1 앱 프로젝트에서 **IAuthenticate** 인터페이스를 구현하는 방법을 보여 줍니다. 동일한 단계가 UWP(유니버설 Windows 플랫폼) 프로젝트에도 적용되지만 **UWP** 프로젝트(명시된 변경 내용 포함)를 사용합니다. Windows 장치를 지원하지 않는 경우 이 섹션을 건너뜁니다.

1. Visual Studio에서 **WinApp** 또는 **WinPhone81** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정**을 클릭합니다.
2. F5 키를 눌러 디버거에서 프로젝트를 실행하고 앱이 시작된 후 상태 코드 401(인증되지 않음)의 처리되지 않은 예외가 발생하는지 확인합니다. 백 엔드에서 액세스를 인증된 사용자만으로 제한했기 때문에 401 응답이 발생합니다.
3. Windows 앱 프로젝트에 대한 MainPage.xaml.cs를 열고 다음 `using` 문을 추가합니다.
   
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;
   
    `<your_Portable_Class_Library_namespace>` 를 이식 가능한 클래스 라이브러리의 네임스페이스로 바꿉니다.
4. 다음과 같이 **IAuthenticate** 인터페이스를 구현하도록 **MainPage** 클래스를 업데이트합니다.
   
        public sealed partial class MainPage : IAuthenticate
5. 다음과 같이 **IAuthenticate** 인터페이스에 필요한 **MobileServiceUser** 필드 및 **Authenticate** 메서드를 추가하여 **MainPage** 클래스를 업데이트합니다.
   
        // Define a authenticated user.
        private MobileServiceUser user;
   
        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;
   
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }
   
            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }
   
            // Display the success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();
   
            return success;
        }

    Facebook 이외의 ID 공급자를 사용하는 경우 [MobileServiceAuthenticationProvider]에 대해 다른 값을 선택합니다.

1. `LoadApplication()`에 대한 호출 이전에 **MainPage** 클래스에 대한 생성자에 다음 코드 줄을 추가합니다.
   
        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);
   
    `<your_Portable_Class_Library_namespace>` 를 이식 가능한 클래스 라이브러리의 네임스페이스로 바꿉니다.
   
    WinApp 프로젝트를 수정하는 경우 8단계로 건너뜁니다. 다음 단계는 WinPhone81 프로젝트에만 적용되며 여기서 로그인 콜백을 완료해야 합니다.
2. (선택 사항) **WinPhone81** 앱 프로젝트에서 App.xaml.cs를 열고 다음 `using` 문을 추가합니다.
   
        using Microsoft.WindowsAzure.MobileServices;
        using <your_Portable_Class_Library_namespace>;
   
    `<your_Portable_Class_Library_namespace>` 를 이식 가능한 클래스 라이브러리의 네임스페이스로 바꿉니다.
3. **WinPhone81** 또는 **WinApp**을 사용하는 경우 **App** 클래스에 다음 **OnActivated** 메서드 재정의를 추가합니다.
   
       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);
   
           // We just need to handle activation that occurs after web authentication.
           if (args.Kind == ActivationKind.WebAuthenticationBrokerContinuation)
           {
               // Get the client and call the LoginComplete method to complete authentication.
               var client = TodoItemManager.DefaultManager.CurrentClient as MobileServiceClient;
               client.LoginComplete(args as WebAuthenticationBrokerContinuationEventArgs);
           }
       }
   
   메서드 재정의가 이미 있는 경우 위의 코드 조각에서 조건부 코드를 추가합니다.  이 코드는 유니버설 Windows 프로젝트에는 필요하지 않습니다.
4. 앱을 다시 빌드하고 실행한 후 선택한 인증 공급자를 사용하여 로그인하고 인증된 사용자로 데이터에 액세스할 수 있는지 확인합니다.

## <a name="next-steps"></a>다음 단계
이 기본 인증 자습서를 완료했으므로 다음 자습서 중 하나를 계속하는 것을 고려해보세요.

* [앱에 푸시 알림 추가](app-service-mobile-xamarin-forms-get-started-push.md)
  
   앱에 푸시 알림 지원을 추가하고 모바일 앱 백 엔드를 구성하여 푸시 알림을 보내는 Azure 알림 허브를 사용하는 방법을 알아봅니다.
* [앱에 오프라인 동기화 사용](app-service-mobile-xamarin-forms-get-started-offline-data.md)
  
  모바일 앱 백 엔드를 사용하여 앱에 오프라인 지원을 추가하는 방법을 알아봅니다. 오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱과 데이터 보기, 추가 또는 수정과 같은 상호 작용을 수행할 수 있습니다.

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx



<!--HONumber=Nov16_HO3-->


