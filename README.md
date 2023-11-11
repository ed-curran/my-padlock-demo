# TrustSight Demo
This repository is a mono-repo containing everything used to construct the TrustSight demo.
The TrustSight demo is of course used to show off [TrustSight](https://github.com/ed-curran/TrustSight) itself, 
but also serves as a proof of concept for the implementation of a trust framework.

In fact, the demo is inspired by reality - The original trust framework is real, and it came first.

Try out the [demo](https://trust-sight-ddiatf.vercel.app/). Or stick around for the story.

## The Story

The [Property Data Trust Framework](https://propdata.org.uk/) (PDTF)
created by the [Home Buying and Selling Group](https://homebuyingandsellinggroup.co.uk/), and now managed by the [Open Property Data Association](https://openpropdata.org.uk/), seeks to enable people and organisation within the UK to exchange trustworthy property data more easily.
Its significant contribution currently is the publication of [data schemas](https://github.com/Property-Data-Trust-Framework/schemas) describing standardised property data.

Recently I've been helping out with the PDTF, thinking about the technical implementation of a trust framework,
and banging on about standards such as w3c [verifiable credentials](https://www.w3.org/TR/vc-data-model/), [DIDs](https://www.w3.org/TR/did-core/), and options for verifiable credential exchange.

Unfortunately, but also excitingly, the development of digital trust frameworks is still quite young.

Another important piece of this tale is the UKs 
[Digital Identity and Attributes Trust Framework](https://www.gov.uk/government/publications/uk-digital-identity-and-attributes-trust-framework-beta-version/uk-digital-identity-and-attributes-trust-framework-beta-version) (DIATF),
a beta policy paper in the UK.
The policy describes the concept of schemes, that would allow industries to create domain specific trust frameworks that are certified by DSIT.

I wanted to find out, from the perspective of the average internet user:
- How could an organisation prove their participation, and role, in the PDTF?
- How could the PDTF prove its certification as a DIATF scheme?

Hence, TrustSight is born.

> TrustSight is a trust overlay for your browser, find out more [here](https://github.com/ed-curran/TrustSight).

But also, a trust framework started to come together, actually, two of them. The trust frameworks only really exists in this demo.

But the tooling to construct trust frameworks started to come together too.

## The Implementation

Each website used in the demo can be thought of as two parts

1. The visual site - What you're familiar with, largely visual decoration for the demonstration,  hosts the backbone.
2. The trust backbone - how the site can be identified, and make trust assertions about others. Largely hidden untill revealed by TrustSIght.

Each site has a NextJS app handling part 1.

The trust backbone is implemented as a single model, where each site is an *entity*. 
The model exists in the `demo-trust-backbone` package, which uses `TrustBench` to build the model into 
pieces that can be hosted by each app, while correctly referencing each other.

[**TrustBench**](packages/trustbench), for me, is the unexpected star of the show, but maybe I just need to lie down. I would recommend you check it out.

### Apps

In each of these readmes you can find more detail about the purpose / inspiration for these entities.

**[Demo Digital Identity and Attributes Trust Framework](apps/docs/README.md) (DDIATF)**

**[Demo Property Data Trust Framework](apps/web/README.md) (DPDTF)**

**Demo Property Pack Provider** (DPPP)

### Packages

[**TrustBench**](packages/trustbench)

A cool build tool thingy I created to help me construct the trust and SSI parts of this demo. 
Namely, DID configurations and trust establishment documents.

**[Demo Trust Backbone](packages/demo-trust-backbone)**

Holds the model defining the trust backbone used by this demo, plus a script to build the model with `TrustBench`
and put the outputs in the right Apps.


## The Boring Stuff
This is turborepo repo (a turbo, repo?). Its mostly typescript.
Frontend is mostly React and Tailwind.

### Utilities

This Turborepo has some additional tools already setup for you:

- [TypeScript](https://www.typescriptlang.org/) for static type checking
- [ESLint](https://eslint.org/) for code linting
- [Prettier](https://prettier.io) for code formatting

### Build

To build all apps and packages, run the following command:

```
pnpm build
```

### Develop

To develop all apps and packages, run the following command:

```
pnpm dev
```


I haven't enabled any of the remote caching stuff, I'm not ready to be Vercel's bitch.

---
### Remote Caching

Turborepo can use a technique known as [Remote Caching](https://turbo.build/repo/docs/core-concepts/remote-caching) to share cache artifacts across machines, enabling you to share build caches with your team and CI/CD pipelines.

By default, Turborepo will cache locally. To enable Remote Caching you will need an account with Vercel. If you don't have an account you can [create one](https://vercel.com/signup), then enter the following commands:

```
npx turbo login
```

This will authenticate the Turborepo CLI with your [Vercel account](https://vercel.com/docs/concepts/personal-accounts/overview).

Next, you can link your Turborepo to your Remote Cache by running the following command from the root of your Turborepo:

```
npx turbo link
```

## Useful Links

Learn more about the power of Turborepo:

- [Tasks](https://turbo.build/repo/docs/core-concepts/monorepos/running-tasks)
- [Caching](https://turbo.build/repo/docs/core-concepts/caching)
- [Remote Caching](https://turbo.build/repo/docs/core-concepts/remote-caching)
- [Filtering](https://turbo.build/repo/docs/core-concepts/monorepos/filtering)
- [Configuration Options](https://turbo.build/repo/docs/reference/configuration)
- [CLI Usage](https://turbo.build/repo/docs/reference/command-line-reference)
