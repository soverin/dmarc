# DMARC

[![Code Climate](https://codeclimate.com/github/trailofbits/dmarc.png)](https://codeclimate.com/github/trailofbits/dmarc) [![Build Status](https://travis-ci.org/trailofbits/dmarc.svg)](https://travis-ci.org/trailofbits/dmarc)
[![Gem Version](https://badge.fury.io/rb/dmarc.svg)](http://badge.fury.io/rb/dmarc)
[![YARD Docs](http://img.shields.io/badge/yard-docs-blue.svg)](http://rubydoc.info/gems/dmarc)
[![Test Coverage](https://codeclimate.com/github/trailofbits/dmarc/badges/coverage.svg)](https://codeclimate.com/github/trailofbits/dmarc)

[DMARC] is a technical specification intended to solve a couple of long-standing
email authentication problems. DMARC policies are described in DMARC "records," 
which are stored as DNS TXT records on a subdomain. This library contains a
parser for DMARC records.

## Example

Parse a SPF record:

    require 'dmarc'

    record = DMARC::Record.parse("v=DMARC1; p=reject; rua=mailto:d@rua.agari.com; ruf=mailto:d@ruf.agari.com; fo=1")

    record.v
    # => :DMARC1

    record.adkim
    # => :r

    record.aspf
    # => :r

    record.fo
    # => ["0"]

    record.p
    # => :reject

    record.pct
    # => 100

    record.rf
    # => :afrf

    record.ri
    # => 86400

    record.rua
    # => [#<URI::MailTo:0x000000034a1cc8 URL:mailto:d@rua.agari.com>]

    record.ruf
    # => [#<URI::MailTo:0x000000034a02b0 URL:mailto:d@ruf.agari.com>]

    record.sp
    # => :reject

Query the SPF record for a domain:

    record = DMARC::Record.query('twitter.com')
    # => #<DMARC::Record:0x0000000313bd90 @adkim=:r, @aspf=:r, @fo=["1"@79], @p=:reject, @pct=100, @rf=:afrf, @ri=86400, @rua=[#<URI::MailTo:0x00000003124e38 URL:mailto:d@rua.agari.com>], @ruf=[#<URI::MailTo:0x00000003132678 URL:mailto:d@ruf.agari.com>], @sp=:reject, @v=:DMARC1>

## Requirements

* [parslet] ~> 1.5

## Install

    $ gem install dmarc

## Testing

To run the RSpec tests:

    $ rake spec

To test the parser against the Alexa Top 500:

    $ rake spec:gauntlet

## License

See the {file:LICENSE.txt} file.

[DMARC]: https://tools.ietf.org/html/rfc7489
[parslet]: http://kschiess.github.io/parslet/
