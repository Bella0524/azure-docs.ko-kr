---
title: "Azure Active Directory B2B 공동 작업의 사용자 토큰 이해 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업에 대한 사용자 토큰 참조"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 02/06/2017
ms.author: sasubram
translationtype: Human Translation
ms.sourcegitcommit: 0c05cd490ee9125f7e5182cb502db6f4e9390094
ms.openlocfilehash: 9eb972d99922676eb2c64dcfa27aad2709d751f0


---


# <a name="understand-user-tokens-in-azure-active-directory-b2b-collaboration"></a>Azure Active Directory B2B 공동 작업의 사용자 토큰 이해

B2B 공동 작업 사용자에 대해 표시되는 토큰 형태에 관심이 있는 경우 다음에 나와 있는 리소스 테넌트(tenantid:04dcc6ab-388a-4559-b527-fbec656300ea)에서 AAD 게스트 및 MSA 게스트에 대한 전달자 토큰 세부 정보 및 토큰 내용을 확인하세요. [https://jwt.io/](https://jwt.io/) 또는 [http://calebb.net](http://calebb.net/)/을 사용하여 JWT 토큰 내용을 볼 수 있습니다.

## <a name="azure-ad-guest-user-token"></a>Azure AD 게스트 사용자 토큰
```
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ilk0dWVLMm9hSU5RaVFiNVlFQlNZVnlEY3BBVSIsImtpZCI6Ilk0dWVLMm9hSU5RaVFiNVlFQlNZVnlEY3BBVSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0LyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzA0ZGNjNmFiLTM4OGEtNDU1OS1iNTI3LWZiZWM2NTYzMDBlYS8iLCJpYXQiOjE0ODQ4MDM5MTgsIm5iZiI6MTQ4NDgwMzkxOCwiZXhwIjoxNDg0ODA3ODE4LCJhY3IiOiIxIiwiYWlvIjoiQVFBQkFBRUFBQURSTllSUTNkaFJTcm0tNEstYWRwQ0pJNWNncGtYQ0VOTHdnN1Z1emhFQURIajNOOWNIMzhRWGFBakhrYUtPRFhneWJpcnVRYVhpa3RZZ3I2M0xMQTVTVDlEeXV2dEtQSUdlXzJpVFRhdjNqSkxuTlRSZ2JWRFpwckhSaEtZbWl5RWdBQSIsImFsdHNlY2lkIjoiNTo6MTAwMzAwMDA4MDFCQUZDNyIsImFtciI6WyJwd2QiLCJyc2EiXSwiYXBwaWQiOiJjNDRiNDA4My0zYmIwLTQ5YzEtYjQ3ZC05NzRlNTNjYmRmM2MiLCJhcHBpZGFjciI6IjIiLCJlX2V4cCI6MTA4MDAsImVtYWlsIjoicmFqZXNiQG1pY3Jvc29mdC5jb20iLCJpZHAiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDcvIiwiaW5fY29ycCI6InRydWUiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTk1IiwibmFtZSI6InJhamVzaCIsIm9pZCI6IjA1ODAyY2M1LTgxMWUtNDZiZC1iMWI2LTU5NDZlNjY4ODIyZiIsInBsYXRmIjoiMyIsInB1aWQiOiIxMDAzM0ZGRjlEOEY5OTUzIiwic2NwIjoidXNlcl9pbXBlcnNvbmF0aW9uIiwic3ViIjoiS1d3QnVCNk5ROU5UYmpoSUI1OHEwM2FlQVl6cEk2TWxiMkpncGk1aV9ITSIsInRpZCI6IjA0ZGNjNmFiLTM4OGEtNDU1OS1iNTI3LWZiZWM2NTYzMDBlYSIsInVuaXF1ZV9uYW1lIjoicmFqZXNiQG1pY3Jvc29mdC5jb20iLCJ2ZXIiOiIxLjAifQ.Vllr1hGXpBlpXDBKRHHYbMr_1_DwKNY3eCObBOfEaxJirwqujqCZodPrAkIOJlFYyhkILyHZQUi_D1w7XoPsd6U4GQlgOoFfzbye-P_NdRFabHMlv32gCgHz1xo11aPP453EiwwG5OHnWaHYLBpuqi3sNeKx06xbTFj07HmADDaR4aM0jwy031d6GkD0LdU-Xkazi5-h8parVRLOkkLZA0oxMFoxl_-VHr1hOzxCkbWgRoug4t97161i5tGil99CcpJ6NK8uQld7TveC40sjJ735Sksn-Uq_NZcJuXCEVsH0xK5evaeFBFSEqACXjKTvYkJWtAx8Kr8yWZAcEg0YMQ
```

## <a name="microsoft-account-guest"></a>Microsoft 계정 게스트
```
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ilk0dWVLMm9hSU5RaVFiNVlFQlNZVnlEY3BBVSIsImtpZCI6Ilk0dWVLMm9hSU5RaVFiNVlFQlNZVnlEY3BBVSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0LyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzA0ZGNjNmFiLTM4OGEtNDU1OS1iNTI3LWZiZWM2NTYzMDBlYS8iLCJpYXQiOjE0ODQ4MDMwNjEsIm5iZiI6MTQ4NDgwMzA2MSwiZXhwIjoxNDg0ODA2OTYxLCJhY3IiOiIxIiwiYWlvIjoiQVFBQkFBRUFBQURSTllSUTNkaFJTcm0tNEstYWRwQ0pEeEd4a3lUdmJ2d1RoSHJnTEdPaGZEbTA1aXJndC1lR1d3YTl5QUZQQTJQc19nZHF2bHQ1X1AtaDhrT2IwdUdza3dyYklBbUhvMEtRM005N2ZCVlRtdzRKY0NfaFVkWW1PZ25QYVlOY1BRQXBIYmFMcUlaZGhaRXhtQVZJeXFmaElBQSIsImFsdHNlY2lkIjoiMTpsaXZlLmNvbTowMDAzMDAwMEEwNzBCOTYyIiwiYW1yIjpbInB3ZCJdLCJhcHBpZCI6ImM0NGI0MDgzLTNiYjAtNDljMS1iNDdkLTk3NGU1M2NiZGYzYyIsImFwcGlkYWNyIjoiMiIsImVfZXhwIjoxMDgwMCwiZW1haWwiOiJiYXNhcmFqZXNoQGxpdmUuY29tIiwiZmFtaWx5X25hbWUiOiJiYXNhIiwiZ2l2ZW5fbmFtZSI6InJhamVzaCIsImlkcCI6ImxpdmUuY29tIiwiaXBhZGRyIjoiMTY3LjIyMC4xLjE5NSIsIm5hbWUiOiJiYXNhcmFqZXNoIiwib2lkIjoiMjU0NmU3NDEtNmZjNi00ZDI0LTg2NTQtZjkyNDc5MzI0ZjM3IiwicGxhdGYiOiIzIiwicHVpZCI6IjEwMDMzRkZGOURBQjk2NDYiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiI4Y2N5OEh4cmE5UTl2aGdYOXhBODFBeWJEV3dsVmxjXzRBZVJYZ2lzamM4IiwidGlkIjoiMDRkY2M2YWItMzg4YS00NTU5LWI1MjctZmJlYzY1NjMwMGVhIiwidW5pcXVlX25hbWUiOiJsaXZlLmNvbSNiYXNhcmFqZXNoQGxpdmUuY29tIiwidmVyIjoiMS4wIn0.LSIBlJpElXpsGXOGaFINW-jOBHsI0Dxe3oX-YIEsccegDCspl6UnRjpwzs0nBL09B4N0oqLd7ZwXZAQURpgaAFnWvROxkIGpNTE_ppSKU1suud8keG5VnTEu82em95G1_c_eW1nOemPvbADCC8h08p2wxNm8QyEhmYqauN6qYbeqOnioRERXO3zOPg8nSXFcGPhvumJ_BW8XKnW4zLdhK78c3PgynPnwtIm08SksMRDzGMgUc9RK1bpPQtgX8iFQByEljf5cuE_h_e1Nr5Y4StrhS3JCiQLTYZ727YY-lSm5DERiQrt7MkP5BHprEmSByofSvACj5TmVdqBFUjobuA
```


## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 공동 작업 사용자 속성](active-directory-b2b-user-properties.md)
* [역할에 B2B 공동 작업 사용자 추가](active-directory-b2b-add-guest-to-role.md)
* [B2B 공동 작업 초대 위임](active-directory-b2b-delegate-invitations.md)
* [동적 그룹 및 B2B 공동 작업](active-directory-b2b-dynamic-groups.md)
* [B2B 공동 작업 코드 및 PowerShell 샘플](active-directory-b2b-code-samples.md)
* [B2B 공동 작업용 SaaS 앱 구성](active-directory-b2b-configure-saas-apps.md)
* [B2B 공동 작업 사용자 클레임 매핑](active-directory-b2b-claims-mapping.md)
* [Office 365 외부 공유](active-directory-b2b-o365-external-user.md)
* [B2B 공동 작업 현재 제한](active-directory-b2b-current-limitations.md)



<!--HONumber=Feb17_HO1-->


