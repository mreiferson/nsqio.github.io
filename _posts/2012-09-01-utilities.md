--- 
title: utilities
layout: post
category: components
permalink: /components/utilities.html
---

These are utilities that facilitate common functionality and introspection into data streams.

### nsq_stat

Polls `/stats` for all the producers of the specified topic/channel and displays aggregate stats

    ---------------depth---------------+--------------metadata---------------
      total    mem    disk inflt   def |     req     t-o         msgs clients
      24660  24660       0     0    20 |  102688       0    132492418       1
      25001  25001       0     0    20 |  102688       0    132493086       1
      21132  21132       0     0    21 |  102688       0    132493729       1

#### Command Line Options

    -channel="": NSQ channel
    -lookupd-http-address=: lookupd HTTP address (may be given multiple times)
    -nsqd-http-address=: nsqd HTTP address (may be given multiple times)
    -status-every=2s: duration of time between polling/printing output
    -topic="": NSQ topic
    -version=false: print version

### nsq_tail

Consumes the specified topic/channel and writes to stdout (in the spirit of tail(1))

#### Command Line Options

    -channel="": NSQ channel
    -consumer-opt=: option to passthrough to nsq.Consumer (may be given multiple times, http://godoc.org/github.com/nsqio/go-nsq#Config)
    -lookupd-http-address=: lookupd HTTP address (may be given multiple times)
    -max-in-flight=200: max number of messages to allow in flight
    -n=0: total messages to show (will wait if starved)
    -nsqd-tcp-address=: nsqd TCP address (may be given multiple times)
    -topic="": NSQ topic
    -version=false: print version string

### nsq\_to_file

Consumes the specified topic/channel and writes out to a newline delimited file, optionally
rolling and/or compressing the file.

#### Command Line Options

    -channel string: nsq channel (default "nsq_to_file")
    -consumer-opt value: option to passthrough to nsq.Consumer (may be given multiple times, http://godoc.org/github.com/nsqio/go-nsq#Config)
    -datetime-format string: strftime compatible format for <DATETIME> in filename format (default "%Y-%m-%d_%H")
    -filename-format string: output filename format (<TOPIC>, <HOST>, <PID>, <DATETIME>, <REV> are replaced. <REV> is increased when file already exists) (default "<TOPIC>.<HOST><REV>.<DATETIME>.log")
    -gzip: gzip output files.
    -gzip-level int: gzip compression level (1-9, 1=BestSpeed, 9=BestCompression) (default 6)
    -host-identifier string: value to output in log filename in place of hostname. <SHORT_HOST> and <HOSTNAME> are valid replacement tokens
    -lookupd-http-address value: lookupd HTTP address (may be given multiple times)
    -max-in-flight int: max number of messages to allow in flight (default 200)
    -nsqd-tcp-address value: nsqd TCP address (may be given multiple times)
    -output-dir string: directory to write output files to (default "/tmp")
    -rotate-interval duration: rotate the file every duration
    -rotate-size rotate-size: rotate the file when it grows bigger than rotate-size bytes
    -skip-empty-files: Skip writing empty files
    -topic value: nsq topic (may be given multiple times)
    -topic-pattern string: Only log topics matching the following pattern (default ".*")
    -topic-refresh duration: how frequently the topic list should be refreshed (default 1m0s)
    -version: print version string

### nsq\_to_http

Consumes the specified topic/channel and performs HTTP requests (GET/POST) to the specified
endpoints.

#### Command Line Options

    -channel="nsq_to_http": nsq channel
    -consumer-opt=: option to passthrough to nsq.Consumer (may be given multiple times, http://godoc.org/github.com/nsqio/go-nsq#Config)
    -content-type="application/octet-stream": the Content-Type used for POST requests
    -get=: HTTP address to make a GET request to. '%s' will be printf replaced with data (may be given multiple times)
    -http-timeout=20s: timeout for HTTP connect/read/write (each)
    -lookupd-http-address=: lookupd HTTP address (may be given multiple times)
    -max-in-flight=200: max number of messages to allow in flight
    -mode="round-robin": the upstream request mode options: multicast, round-robin, hostpool
    -n=100: number of concurrent publishers
    -nsqd-tcp-address=: nsqd TCP address (may be given multiple times)
    -post=: HTTP address to make a POST request to.  data will be in the body (may be given multiple times)
    -sample=1: % of messages to publish (float b/w 0 -> 1)
    -status-every=250: the # of requests between logging status (per handler), 0 disables
    -topic="": nsq topic
    -version=false: print version string

### nsq\_to_nsq

Consumes the specified topic/channel and re-publishes the messages to destination `nsqd` via TCP.

#### Command Line Options

    -channel="nsq_to_nsq": nsq channel
    -consumer-opt=: option to passthrough to nsq.Consumer (may be given multiple times, see http://godoc.org/github.com/nsqio/go-nsq#Config)
    -destination-nsqd-tcp-address=: destination nsqd TCP address (may be given multiple times)
    -destination-topic="": destination nsq topic
    -lookupd-http-address=: lookupd HTTP address (may be given multiple times)
    -max-in-flight=200: max number of messages to allow in flight
    -mode="round-robin": the upstream request mode options: round-robin (default), hostpool
    -nsqd-tcp-address=: nsqd TCP address (may be given multiple times)
    -producer-opt=: option to passthrough to nsq.Producer (may be given multiple times, see http://godoc.org/github.com/nsqio/go-nsq#Config)
    -require-json-field="": for JSON messages: only pass messages that contain this field
    -require-json-value="": for JSON messages: only pass messages in which the required field has this value
    -status-every=250: the # of requests between logging status (per destination), 0 disables
    -topic="": nsq topic
    -version=false: print version string
    -whitelist-json-field=: for JSON messages: pass this field (may be given multiple times)

### to_nsq

Takes a stdin stream and splits on newlines (default) for re-publishing to destination `nsqd` via
TCP.

#### Command Line Options

    -delimiter="\n": character to split input from stdin (defaults to '\n')
    -nsqd-tcp-address=: destination nsqd TCP address (may be given multiple times)
    -producer-opt=: option to passthrough to nsq.Producer (may be given multiple times, http://godoc.org/github.com/nsqio/go-nsq#Config)
    -topic="": NSQ topic to publish to
