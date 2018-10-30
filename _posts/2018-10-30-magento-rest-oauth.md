---
published: false
---
## [Как включить создание токенов для API](https://magento.stackexchange.com/questions/178843/cannot-create-oauth-consumer):

I figured out my issue. In **System -> Configuration -> Advanced -> Advanced**, I had to enable Mage OAuth. Then I had to go to **System -> Cache Management** and run Flush Magento Cache. I was unaware that settings and modules for the actual admin dashboard would also be cached and not automatically flushed when settings are updated.
