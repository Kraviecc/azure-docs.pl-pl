---
title: Korzystanie z usługi Active Learning z bazą wiedzy QnA Maker
description: Dowiedz się, jak poprawić jakość bazy wiedzy dzięki aktywnej uczeniu. Przeglądanie, akceptowanie lub odrzucanie, Dodawanie bez usuwania lub zmieniania istniejących pytań.
ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: conceptual
ms.date: 03/18/2020
ms.openlocfilehash: 396cba079baf92da1f5d14a4ecf3dfdb7de0aa2f
ms.sourcegitcommit: b85ce02785edc13d7fb8eba29ea8027e614c52a2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/03/2021
ms.locfileid: "99509234"
---
# <a name="use-active-learning-to-improve-your-knowledge-base"></a>Ulepszanie bazy wiedzy za pomocą uczenia aktywnego

[Usługa Active Learning](../Concepts/active-learning-suggestions.md) pozwala ulepszyć jakość bazy wiedzy, sugerując inne pytania. Zgłoszenia użytkowników są brane pod uwagę i są wyświetlane w postaci sugestii na liście pytań alternatywnych. Aby dodać te sugestie jako pytania alternatywne lub je odrzucić, możesz to zrobić.

Baza wiedzy nie zmienia się automatycznie. Aby zmiany zaczęły obowiązywać, należy zaakceptować sugestie. Te sugestie dodają pytania, ale nie zmieniają ani nie usuwają istniejących pytań.

## <a name="upgrade-runtime-version-to-use-active-learning"></a>Uaktualnij wersję środowiska uruchomieniowego, aby użyć usługi Active Learning

# <a name="qna-maker-ga-stable-release"></a>[QnA Maker GA (wersja stabilna)](#tab/v1)

Usługa Active Learning jest obsługiwana w środowisku uruchomieniowym w wersji 4.4.0 i nowszych. Jeśli baza wiedzy została utworzona w starszej wersji, [Uaktualnij środowisko uruchomieniowe](set-up-qnamaker-service-azure.md#get-the-latest-runtime-updates) , aby użyć tej funkcji.

# <a name="qna-maker-managed-preview-release"></a>[Zarządzane QnA Maker (wersja zapoznawcza)](#tab/v2)

W QnA Maker Managed (wersja zapoznawcza), ponieważ środowisko wykonawcze jest hostowane przez usługę QnA Maker, nie ma potrzeby ręcznego uaktualniania środowiska uruchomieniowego.

---

## <a name="turn-on-active-learning-for-alternate-questions"></a>Włącz aktywną naukę w przypadku pytań alternatywnych

# <a name="qna-maker-ga-stable-release"></a>[QnA Maker GA (wersja stabilna)](#tab/v1)

Aktywna nauka jest domyślnie wyłączona. Włącz tę opcję, aby zobaczyć sugerowane pytania. Po włączeniu aktywnego uczenia należy wysłać informacje z aplikacji klienckiej do QnA Maker. Aby uzyskać więcej informacji, zobacz temat [Architektura przepływu na potrzeby używania GenerateAnswer i uczenia interfejsów API z bot](improve-knowledge-base.md#architectural-flow-for-using-generateanswer-and-train-apis-from-a-bot).

1. Wybierz pozycję **Publikuj** , aby opublikować bazę wiedzy. Aktywne zapytania szkoleniowe są zbierane tylko z punktu końcowego przewidywania interfejsu API GenerateAnswer. Zapytania do okienka test w portalu QnA Maker nie wpływają na aktywną naukę.

1. Aby włączyć aktywną naukę w portalu QnA Maker, przejdź do prawego górnego rogu, wybierz swoją **nazwę** i przejdź do pozycji [**Ustawienia usługi**](https://www.qnamaker.ai/UserSettings).

    ![Na stronie ustawień usługi Włącz zaproponowane wątpliwości dotyczące aktywnego uczenia. Wybierz swoją nazwę użytkownika w prawym górnym menu, a następnie wybierz pozycję Ustawienia usługi.](../media/improve-knowledge-base/Endpoint-Keys.png)


1. Znajdź usługę QnA Maker a następnie Przełącz **aktywną naukę**.

    > [!div class="mx-imgBorder"]
    > [![Na stronie Ustawienia usługi Przełącz funkcję Active Learning. Jeśli nie możesz przełączać tej funkcji, może być konieczne uaktualnienie usługi.](../media/improve-knowledge-base/turn-active-learning-on-at-service-setting.png)](../media/improve-knowledge-base/turn-active-learning-on-at-service-setting.png#lightbox)

    > [!Note]
    > Dokładna wersja na powyższym obrazie jest pokazywana tylko jako przykład. Twoja wersja może być inna.

    Po włączeniu **aktywnej uczenia** baza wiedzy sugeruje nowe pytania w regularnych odstępach czasu na podstawie pytań przesłanych przez użytkownika. **Aktywną naukę** można wyłączyć, przełączając ponownie ustawienie.
    
# <a name="qna-maker-managed-preview-release"></a>[Zarządzane QnA Maker (wersja zapoznawcza)](#tab/v2)

Domyślnie usługa Active Learning jest **włączona** w QNA Maker Managed (wersja zapoznawcza). Aby wyświetlić sugerowane pytania alternatywne, [Użyj opcji wyświetlania](../How-To/improve-knowledge-base.md#view-suggested-questions) na stronie Edycja.

---

## <a name="review-suggested-alternate-questions"></a>Przejrzyj sugerowane pytania alternatywne

Zapoznaj się z [alternatywnymi sugerowanymi pytaniami](improve-knowledge-base.md) na stronie **edytowania** każdej bazy wiedzy.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Tworzenie bazy wiedzy](./manage-knowledge-bases.md)
