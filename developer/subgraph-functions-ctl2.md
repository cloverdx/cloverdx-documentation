<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Subgraph functions -->

### Subgraph functions

#### List of Functions

| [getSubgraphInputPortsCount](subgraph-functions-ctl2.md#getsubgraphinputportscount) |
| --- |
| [getSubgraphOutputPortsCount](subgraph-functions-ctl2.md#getsubgraphoutputportscount) |
| [isSubgraphInputPortConnected](subgraph-functions-ctl2.md#issubgraphinputportconnected) |
| [isSubgraphOutputPortConnected](subgraph-functions-ctl2.md#issubgraphoutputportconnected) |

Subgraph functions let user acquire details on input and output ports of subgraph.

These functions are only available in subgraphs. If you use them out of a subgraph, the functions fail.

If you work with subgraphs, you may need parse mapping. See [Mapping Functions](mapping-functions-ctl2.md).

#### getSubgraphInputPortsCount

```ctl
integer getSubgraphInputPortsCount();
```

The function `getSubgraphInputPortsCount()` returns the number of input ports.

**Compatibility**

The function `getSubgraphInputPortsCount()` is available since **CloverETL 4.1.0**.
Example 349. Usage of getSubgraphInputPortsCount There is a subgraph having two input ports and one output port. The function `getSubgraphInputPortsCount()` returns `2`.
**See also:**[getSubgraphOutputPortsCount](subgraph-functions-ctl2.md#getsubgraphoutputportscount), [isSubgraphInputPortConnected](subgraph-functions-ctl2.md#issubgraphinputportconnected), [isSubgraphOutputPortConnected](subgraph-functions-ctl2.md#issubgraphoutputportconnected)

#### getSubgraphOutputPortsCount

```ctl
integer getSubgraphOutputPortsCount();
```

The function `getSubgraphOutputPortsCount()` returns the number of output ports.

**Compatibility**

The function `getSubgraphOutputPortsCount()` is available since **CloverETL 4.1.0**.
Example 350. Usage of getSubgraphOutputPortsCount There is a subgraph having two input ports and one output port. The function `getSubgraphOutputPortsCount()` returns `1`.
**See also:**[getSubgraphInputPortsCount](subgraph-functions-ctl2.md#getsubgraphinputportscount), [isSubgraphInputPortConnected](subgraph-functions-ctl2.md#issubgraphinputportconnected), [isSubgraphOutputPortConnected](subgraph-functions-ctl2.md#issubgraphoutputportconnected)

#### isSubgraphInputPortConnected

```ctl
boolean isSubgraphInputPortConnected(integer portNo);
```

The function `isSubgraphInputPortConnected()` returns `true` if the particular subgraph input port is connected. Otherwise, it returns `false`.

Port numbers start from zero.

If `portNo` is not a valid port number of a particular subgraph (negative value or too big value), the function fails with an error.

**Compatibility**

The `isSubgraphInputPortConnected()` function is available since **CloverETL 4.1.0**.
Example 351. Usage of isSubgraphInputPortConnected
There is a subgraph having two input ports: the first one is connected, the second one is not connected.

The function `isSubgraphInputPortConnected(0)` returns `true`.

The function `isSubgraphInputPortConnected(1)` returns `false`.

The function `isSubgraphInputPortConnected(2)` fails.

**See also:**[getSubgraphInputPortsCount](subgraph-functions-ctl2.md#getsubgraphinputportscount), [getSubgraphOutputPortsCount](subgraph-functions-ctl2.md#getsubgraphoutputportscount), [isSubgraphOutputPortConnected](subgraph-functions-ctl2.md#issubgraphoutputportconnected)

#### isSubgraphOutputPortConnected

```ctl
boolean isSubgraphOutputPortConnected(integer portNo);
```

The function `isSubgraphOutputPortConnected()` returns `true` if the particular subgraph output port is connected. Otherwise, it returns `false`.

Port numbers start from zero.

If `portNo` is not a valid port number of a particular subgraph (negative value or too big value), the function fails with an error.

**Compatibility**

The `isSubgraphOutputPortConnected()` function is available since **CloverETL 4.1.0**.
Example 352. Usage of isSubgraphOutputPortConnected
There is a subgraph having two output ports: the first one is connected, the second one is not connected.

The function `isSubgraphOutputPortConnected(0)` returns `true`.

The function `isSubgraphOutputPortConnected(1)` returns `false`.

The function `isSubgraphOutputPortConnected(2)` fails.

**See also:**[getSubgraphInputPortsCount](subgraph-functions-ctl2.md#getsubgraphinputportscount), [getSubgraphOutputPortsCount](subgraph-functions-ctl2.md#getsubgraphoutputportscount), [isSubgraphInputPortConnected](subgraph-functions-ctl2.md#issubgraphinputportconnected)
