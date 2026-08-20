Where: [Google Feedback](https://www.google.com/tools/feedback)

Who: Google account 沈威宇 cg10250207@gmail.com

---

## Suggestion: Respect the "Accept-Language" HTTP Header

### Expected Behavior

When a user sends "Accept-Language" HTTP Header, Google should use that language by default and possibly provide the one inferred from IP geolocation or other means in the "Google offered in <language>".

For example, if a browser sends: "Accept-Language: en-US,en;q=0.9". Google should preferably serve the English version of the page, even if the user's IP address indicates a different region.

### Current Behavior

Google's services mainly use language inferred from IP geolocation by default and offer the one requested by "Accept Language" HTTP Header in "Google offered in <language>" in some but not all of the services.

### Benefit

The current behavior makes it inconvenient for users whose preferred languages are not the languages inferred by IP geolocation and who use browsers without saving cookies. This inconsistency may be due to traveling, using a VPN, living in a region where their preferred interface language differs from the local language, or, in my case, the fact that I learn programming and develop and write documentation for software in English. Thus, please consider giving the "Accept-Language" HTTP header greater priority when determining the language of Google's services.

