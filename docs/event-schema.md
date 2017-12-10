# Event schema

Our data model for events is based on the [Event Object](http://docs.opencivicdata.org/en/latest/data/event.html) from the [Open Civic Data](http://docs.opencivicdata.org) project.

For our initial scrapers, we are focusing on basic event data. Over time, this
may expand to include meeting notes, agendas, etc.

```python
{
  '_type': 'event',                              # required value
  'id': 'unique identifier'                      # required string in format:
                                                 # <spider-name>/<start-time-in-YYYYMMddhhmm>/<unique-id>/<underscored-event-name>
  'name': 'Committee on Pedestrian Safety',      # required string
  'description': 'A longer description',         # optional string
  'classification': 'Public Safety'              # general topic of the meeting
  'start_time': '2017-08-30T17:30:00Z',          # required datetime in UTC, using ISO8601 format
  'end_time': None,                              # optional datetime in UTC, using ISO8601 format
  'timezone': 'America/Chicago',                 # required timezone in tzinfo format
  'all_day': False,                              # must be True or False

  'location': {                                  # required dictionary
    'url': '',                                   # optional URL of the location, not the event!
    'name': 'Room 201A, City Hall, Chicago, IL', # required address of the location
    'coordinates': {                             # must be: None or object
      'latitude': '',                            # empty string; will be filled in by geocoder
      'longitude': ''                            # empty string; will be filled in by geocoder
    }
  },

  'sources': [                                   # required list of sources
    {
      'url': '',                                 # required URL where data was scraped from
      'note': ''                                 # optional info about how the data was scraped
    }
  ]
}
```