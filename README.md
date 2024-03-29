# base-log-factory

[![npm package](https://nodei.co/npm/base-log-factory.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/base-log-factory)

> Pluggable logging utility.

[![NPM version](https://img.shields.io/npm/v/base-log-factory.svg?style=flat)](https://npmjs.org/package/base-log-factory)
[![NPM Downloads](https://img.shields.io/npm/dm/base-log-factory.svg?style=flat)](https://npmjs.org/package/base-log-factory)

## Installation

```bash
npm install --save base-log-factory
```

## Usage

```js
import { createFactory } from 'base-log-factory';

const factory = createFactory();

const logger = factory.getLogger('name');
logger.info('hello');

const logger = factory.getLogger('name2');
logger.error('hello2');
```

## API

```ts
export interface IAppender {
  log(messages: any[], logOpts: LogOptions): void;
  dispose(): Promise<void>;
}

export type TLogLevel = 'ALL' | 'TRACE' | 'DEBUG' | 'INFO' | 'WARN' | 'ERROR' | 'FATAL' | 'OFF';

export interface LoggerOptions {
  level?: TLogLevel;
  appender?: IAppender | IAppender[];
}

export interface LogOptions {
  level: string;
  method: string;
  date: Date;
  name: string;
}

export interface AppenderOptions {
  [key: string]: any;
  layout?: (messages: any[], logOpts: LogOptions) => any[];
}

export interface ILogger {
  name: string;
  level(l?: TLogLevel): TLogLevel | void;
  trace(...args: any[]): void;
  debug(...args: any[]): void;
  info(...args: any[]): void;
  warn(...args: any[]): void;
  error(...args: any[]): void;
  fatal(...args: any[]): void;
}

export interface IFactory {
  getLogger(name?: string): ILogger;
  setLevel(level: TLogLevel): void;
  clear(): void;
}

export declare function format(date: Date, inputString?: string): string;

export declare function createAppender(opts?: AppenderOptions): IAppender;

export declare function createFactory(opts?: LoggerOptions): IFactory;

```