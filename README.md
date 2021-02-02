# CEFS: CentOS Errata for Spacewalk

## Overview

This repository contains my work around CEFS.
It currently consists of the following pieces:

- _errata-import.pl_: The import script that will read XML and write to Spacewalk (or a compatible) API
- _errata-wipe.pl_: A script to remove all existing errata data from Spacewalk (or a compatible) API
- _xml2json.pl_: A script to convert the ugly XML data structure into a nicer JSON form.
- _yum-history-html.pl_: A script to convert the YUM history into HTML and enrich it with errata information.

- _errata.latest.xml_: The latest information on Errata for CentOS (supported versions only)
- _errata.latest.json_: The same data as in the XML, but in JSON format (a derivative)

## Schema

### JSON

```typescript
interface Errata {
  advisories: Array<{
    description: string;
    /**
     * @example ""email@steve-meier.de"
     */
    from: string;
    /**
     * @example "CESA-2021:0150"
     */
    id: string;
    /**
     * @example "2021-01-19 00:00:00"
     */
    issue_date: string;
    /**
     * @example "1"
     */
    manual: string;
    notes: string;
    /**
     * @example ["x86_64", "i686"]
     */
    os_arch?: Maybe<string[]>;
    /**
     * Specifies the major release (7.x, 8.x) an errata applies to. Scraped from the filename (ex. `el7` for major release 7)
     * @example ["7"]
     */
    os_release: string[];
    /**
     * @example ["thunderbird-78.6.1-1.el7.centos.src.rpm"]
     */
    packages: string[];
    product: string;
    /**
     * @example "https://access.redhat.com/errata/RHSA-2021:0087 https://lists.centos.org/pipermail/centos-announce/2021-January/048244.html"
     */
    references: string;
    release: string;
    solution: string;
    synopsis: string;
    topic: string;
    /**
     * @example "Security Advisory"
     */
    type: string;
  }>;
}
```

## License

The data files (errata.latest.xml and errata.latest.json) are licensed CC BY-NC-ND.

See https://creativecommons.org/licenses/by-nc-nd/4.0/

The most recent versions of the data files can be found on the project homepage
at https://cefs.steve-meier.de. The versions in this repository may be outdated.

Any scripts in this repository are licensed under the MIT License.
