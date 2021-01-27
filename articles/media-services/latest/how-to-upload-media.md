---
title: przekazywanie nośnika: Azure Media Services opis: informacje dotyczące przekazywania multimediów do przesyłania strumieniowego lub kodowania.
usługi: Media-Services documentationcenter: "" Author: IngridAtMicrosoft Manager: femila Editor: ""

MS. Service: Media-Services MS. obciążenie: MS. temat: How-to MS. Date: 08/31/2020 MS. Author: inhenkel
---

# <a name="upload-media-for-streaming-or-encoding"></a>Przekazywanie multimediów do przesyłania strumieniowego lub kodowania

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

W Media Services można przekazać pliki cyfrowe (Multimedia) do kontenera obiektów BLOB skojarzonego z elementem zawartości. Jednostka [zasobu](/rest/api/media/operations/asset) może zawierać wideo, audio, obrazy, kolekcje miniatur, ścieżki tekstowe i pliki napisów (oraz metadane dotyczące tych plików). Gdy pliki zostaną przekazane do kontenera zasobów, zawartość jest bezpiecznie przechowywana w chmurze w celu dalszej przetwarzania i przesyłania strumieniowego.

Przed rozpoczęciem pracy należy zebrać lub myśleć o kilku wartościach.

1. Lokalna ścieżka pliku do pliku, który chcesz przekazać
1. Identyfikator elementu zawartości dla elementu zawartości (kontenera)
1. Nazwa, która ma być używana dla przekazanego pliku, łącznie z rozszerzeniem.
1. Nazwa konta magazynu, z którego korzystasz
1. Klucz dostępu do konta magazynu

## <a name="portal"></a>[Portal](#tab/portal/)

[!INCLUDE [Upload files with the portal](./includes/task-upload-file-to-asset-portal.md)]

## <a name="cli"></a>[Interfejs wiersza polecenia](#tab/cli/)

[!INCLUDE [Upload files with the portal](./includes/task-upload-file-to-asset-cli.md)]

## <a name="rest"></a>[REST](#tab/rest/)

Po [utworzeniu elementu zawartości przy użyciu programu Poster lub innej metody REST i uzyskać adres URL sygnatury dostępu współdzielonego dla elementu zawartości](how-to-create-asset.md?tabs=rest)Użyj interfejsów API usługi Azure Storage lub zestawów SDK (na przykład [interfejsu API REST magazynu](../../storage/common/storage-rest-api-auth.md) lub [zestawu SDK platformy .NET](../../storage/blobs/storage-quickstart-blobs-dotnet.md)).

---
<!-- add these to the tabs when available -->
Aby zapoznać się z innymi metodami, zobacz [dokumentację usługi Azure Storage](../../storage/blobs/index.yml) służącą do pracy z obiektami BLOB w językach [.NET](../../storage/blobs/storage-quickstart-blobs-dotnet.md), [Java](../../storage/blobs/storage-quickstart-blobs-java.md), [Python](../../storage/blobs/storage-quickstart-blobs-python.md)i [JavaScript (Node.js)](../../storage/blobs/storage-quickstart-blobs-nodejs.md).

## <a name="next-steps"></a>Następne kroki

> [Przegląd Media Services](media-services-overview.md)