# Microformats2 Utilities

[![Build Status](https://travis-ci.org/kylewm/mf2util.svg?branch=master)](https://travis-ci.org/kylewm/mf2util)

## Datetimes

The `mf2util.parse_dt` function is useful for parsing microformats2
dates and datetimes. It can be used as a microformats-specific
alternative to larger, more general libraries like python-dateutil.

The definition for microformats2 dt-* properties are fairly lenient.
This module will convert a mf2 date string into either a datetime.date
or datetime.datetime object. Datetimes will be naive unless a timezone
is specified.

Timezones are specified as fixed offsets from UTC.

### Usage

```python
import mf2py
import mf2util

parsed = mf2py.Parser(url=…)
publishedstr = parsed.to_dict()['items'][0]['properties']['published'][0]
published = mf2util.parse_dt(published)  # --> datetime.datetime
```

## Mentions

When processing an incoming webmention, you can use the
`mf2util.classify_mentions` method to classify it as a reply, like, or
repost (or a combination thereof). The method returns a list of zero
or more strings (one of 'like', 'repost', or 'reply').

### Usage

```python
import mf2py
import mf2util

# receive webmention from source_url to target_url
target_url = 'http://my-domain.com/2014/04/12/1'
alternate_url = 'http://doma.in/V4ls'
parsed = mf2py.Parser(url=source_url)
mentions = mf2util.find_mentions(parsed, [target_url, alternative_url])
```

## Authorship

Use `mf2py.find_author` to determine an h-event's author name, url,
and photo. Uses the
[authorship algorithm](https://indiewebcamp.com/authorship) described
on the IndieWebCamp wiki.
