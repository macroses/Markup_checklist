 ### Тестирование и валидность
 
 Браузеры

Верстка должна быть протестирована во всех основных браузерах:

    Google Chrome одной из последних версий (от версии 100)
    Firefox (от версии )
    Google Chrome for Android и Android WebView (например, когда ссылка открывается прямо в приложении с использованием встроенного «браузера»)
    Safari for Mac OS
    Safari for iOS
    Safari Web View
    Google Chrome for iOS
    Edge (в одной из последних версий)

TODO: определиться со списком и версиями поддерживаемых браузеров.
Lighthouse

Lighthouse — один из основных средств тестирования производительности, доступности и прочих параметров. Воспользоваться им можно из Chrome DevTools → Lighthouse.

Для проверки страницы в Lighthouse, нужно:

    перейти на вкладку, установить все необходимые чекбоксы для проверки в разделе Categories, обычно это все чекбоксы кроме Progressive Web App, если страница не является PWA.
    выбрать тестирование Mobile или Desktop в разделе Device. Нужно проверять и то и другое по очереди запуская создание отчета.
    запустить создание отчета нажав на кнопку Generate report.



После создания отчета Lighthouse покажет количество баллов по отмеченным категориям проверки и подскажет, что нужно улучшить, чтобы повысить баллы, если они не удовлетворяют требованиям.

Как в мобильном так и в десктопном варианте проверки страница должна набирать не меньше 90 баллов, но для Accessibility и SEO нужно добиваться максимального значения.



Аудит производительности (Performance)

Анализирует параметры производительности:

    Первая отрисовка контента (FCP — First Contentful Paint)
    Общее время блокировки (TBT — Total Blocking Time)
    Скорость загрузки основного контента (LCP — Largest Contentful Paint)
    Совокупное смещение макета (CLS — Cumulative Layout Shift)

Важно понимать, что Lighthouse использует уменьшение скорости и увеличение времени отклика страницы для тестирования в режиме Mobile, чтобы создать максимально похожие условия просмотра тестируемой страницы на мобильном устройстве при меньшей скорости интернета. Lighthouse использует такие условия задержки и пропускной способности для проверки Device → Mobile:

Latency: 150ms
Throughput: 1.6Mbps down / 750 Kbps up.
Packet loss: none.

Если задача стоит в максимальной оптимизации страницы, то качество и скорость загрузки страницы стоит проверять и на меньших пропускных способностях канала.

Необходимые ограничения можно выставить в разделе Network:


Выбрав Slow 3G или добавив свои ограничения в разделе Custom.

Fast 3G и Slow 3G соответствуют таким ограничениям соответственно:

Download 1500 kb/s = 1.5 Mb/s,
Latency = 550 ms

Download 376 kb/s,
Latency 2000 ms

Дополнительно тестировать производительность при таких ограничениях можно на вкладке Performance. Предварительно удалив из дома body, чтобы очистить вьюпорт браузера, с которого будут сниматься скриншоты по мере загрузки страницы. Чтобы запустить запись и тестирование, нужно нажать на кнопку перезагрузки:


Сжатие gzip

Не лишним будет убедиться, что для hmtl-, css- и js-файлов на сервере включено gzip-сжатие.

Это можно проверить по наличию заголовка Content-Encoding: gzip в разделе Response Headers, кликнув на детали документа страницы во вкладке Network.

А также задержав курсор мыши на файле документа во вкладке Network до появления информационного попапа со сравнением количества переданных данных и размера самого файла документа. Если количество данных сильно отличается от испходного документа в меньшую сторону, значит gzip на сервере включен:

Если эти значения практически равны, то gzip не включен:

Глубже о мероприятиях по ускорению загрузки можно ознакомиться в гайде: https://web.dev/fast/


Дополнительные материалы: 

Хороший гайд по подключению шрифтов с отложенной загрузкой CSS, если критично максимально уменьшить время загрузки страницы https://css-tricks.com/how-to-load-fonts-in-a-way-that-fights-fout-and-makes-lighthouse-happy/

и список ссылок в ней:

Устраните ресурсы, блокирующие рендеринг https://web.dev/render-blocking-resources/

Оптимизация загрузки и рендеринга веб-шрифтов https://web.dev/optimize-webfont-loading/

Render Blocking CSS https://web.dev/critical-rendering-path-render-blocking-css/

CSS Basics: Fallback Font Stacks for More Robust Web Typography https://css-tricks.com/css-basics-fallback-font-stacks-robust-web-typography/

Сервис для сравнения шрифтов, и подбора максимально похожего, чтобы минимизировать значение метрики CLS: https://meowni.ca/font-style-matcher/
Аудит доступности (Accessibility)

Доступность в Lighthouse тестируется исходя из гайда:  https://web.dev/lighthouse-accessibility/
Аудит применения лучших практик (Best Practces)

Подробнее об этом аудите можно узнать из гайда: https://web.dev/lighthouse-best-practices/
Аудит применения SEO

Если было учтено большинство требований из раздела Организация кода и процесса разработки, то, как правило, аудит SEO будет пройдет с максимальным баллом.

Более подробно мероприятия по обеспечению оптимизации для поисковых систем описан в разделе https://developers.google.com/search/docs/advanced/guidelines/webmaster-guidelines

Не будет лишним изучить рекомендации Яндекса https://yandex.ru/support/webmaster/yandex-indexing/rank.html