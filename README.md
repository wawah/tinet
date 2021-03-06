
# TINet (Tulip Indicators .NET Wrapper)

## Introduction

TINet is a .NET wrapper for Tulip Indicators that provides access to all the
technical analysis functions from the [Tulip Indicators](https://tulipindicators.org) library.

## Example Usage

In Visual Studio, create a new C# console application.

Add a reference to `tinet.dll`.

All TINet indicators have the same interface. They take an array of inputs, an array of options, and an array of outputs.

Simple Moving Average example:

```C#
//Run SMA on close prices using a smoothing period of 4 bars.

double[] close_prices = new double[] {5, 4, 5, 4, 4, 6, 5, 4, 5, 2, 5, 5, 5, 4, 4, 3};
double[] options = new double[] {4};

//Find output size and allocate output space.
int output_length = close_prices.Length - tinet.indicators.sma.start(options);
double[] output = new double[output_length];

double[][] inputs = { close_prices };
double[][] outputs = { output };
int success = tinet.indicators.sma.run(inputs, options, outputs);

Console.WriteLine("Input bars:");
Console.WriteLine(string.Join(",", close_prices));

Console.WriteLine("SMA Output:");
Console.WriteLine(string.Join(",", output));

Console.WriteLine("Press any key to continue.");
Console.ReadKey();
```


Indicators that take more inputs, options, or outputs have exactly the same interface. You simply need to pass in the extra parameters.

You can find the expected parameters at https://tulipindicators.org or you can see them programatically like so:

```C#
Console.WriteLine(string.Join(", ", tinet.indicators.stoch.inputs()));  // high, low, close
Console.WriteLine(string.Join(", ", tinet.indicators.stoch.options())); // %k period, %k slowing period, %d period
Console.WriteLine(string.Join(", ", tinet.indicators.stoch.outputs())); // stoch_k, stoch_d
```


```C#
//Call Stochastic Oscillator, taking 3 inputs, 3 options, and 2 outputs.
//Assuming high, low, and close are input arrays.

double[] options = new double[] {5, 3, 3};
int output_length = close.Length - tinet.indicators.stoch.start(options);

double[] stoch_k = new double[output_length];
double[] stoch_d = new double[output_length];


double[][] inputs = {high, low, close};
double[][] outputs = {stoch_k, stoch_d};
int success = tinet.indicators.stoch.run(inputs, options, outputs);
```
