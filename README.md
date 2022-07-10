![App screenshot](/public/og-image.png)

# elektronik-timetable ("Plan lekcji express") - a modern school timetable frontend

- Displays data based on static table-style web pages generated by [VULCAN Optivum](https://www.vulcan.edu.pl/programy/plan-lekcji-optivum-23)
- Crafted for [Zespół Szkół Elektronicznych w Rzeszowie](https://www.elektronik.rzeszow.pl/) technical high school from Rzeszow, Poland
- Mobile-first design made to match the school's website one
- Can run for many other Optivum-based school timetables too!
- Data scraping & parsing via [@wulkanowy/timetable-parser-js](https://github.com/wulkanowy/timetable-parser-js)
- Technologies: React, Next.js, TypeScript, Tailwind CSS

# Getting started & preparing the timetable to use with the app

## Environment variables

After cloning the repo, define the environment variables (.env), depending on the method below that you're going to use:

`NEXT_PUBLIC_TIMETABLE_BASE_URL` - timetable base URL: all methods

👉 A timetable base URL is a one that points to a folder in the server containing the timetable list - a "lista.html" file.

`NEXT_PUBLIC_PROXY_URL` - CORS Anywhere proxy URL - method 2 only

## Method 1 - original website

In this method we're going to use the original timetable hosted on your school's website.

Simply define the `NEXT_PUBLIC_TIMETABLE_BASE_URL` env variable with the timetable base URL, such as `https://elektronik.rzeszow.pl/plan-lekcji-2`.

In some cases, the timetable may not fetch to this app due to CORS issues. Use method 2 then.

## Method 2 - original website and CORS Anywhere proxy

It's the same as method 1, but we're adding a CORS Anywhere proxy server to clear all CORS-related issues while fetching the timetable from the school servers. Don't worry, there are no sensitive data passing through, it's just a timetable 😅. However if security is your #1 priority use method 3.

As in method 1 - define the `NEXT_PUBLIC_TIMETABLE_BASE_URL` env variable with the timetable base URL, such as `https://elektronik.rzeszow.pl/plan-lekcji-2`.

Then deploy a CORS Anywhere instance.

Before deploying your instance, set `requireHeader` in its config file to `[]`.

Check out if CORS Anywhere works by proxying your school's timetable base URL like so: `http://<cors_anywhere_url>/https://www.elektronik.rzeszow.pl/plan-lekcji-2`.

You should see two frames with "Not Found" errors. That's okay.

Then, define the `NEXT_PUBLIC_PROXY_URL` env variable with the proxy URL.

If there are problems with SSL, add `process.env['NODE_TLS_REJECT_UNAUTHORIZED'] = '0';` to the top of the CORS Anywhere config file and restart the proxy instance.

## Method 3 - clone and self-serve on an external server

You can also clone the whole timetable and host it on your own server. Useful if you don't want to have automatic timetable updates or if you have CORS issues but the CORS proxy decreases the loading speed.

This way you don't have to worry about CORS Anywhere proxying and related issues, provided if you set up proper CORS handling.

However, you'll lose any automatic updates of the timetable. Be sure to check the original website frequently for any updates.

To clone the website, run `wget -mpEk <timetable_base_url> --no-check-certificate`

Example: `wget -mpEk https://www.elektronik.rzeszow.pl/plan-lekcji-2 --no-check-certificate`

Then, define the `NEXT_PUBLIC_TIMETABLE_BASE_URL` env variable with the timetable base URL, such as `https://dummy-server.dev/timetable-to-serve`.

## .env example

```
NEXT_PUBLIC_PROXY_URL=http://localhost:8080
NEXT_PUBLIC_TIMETABLE_BASE_URL=https://www.elektronik.rzeszow.pl/plan-lekcji
```

## Startup

Then you can install the packages & run the app:

```bash
yarn
yarn dev
```
