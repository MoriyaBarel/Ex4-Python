# Ex4-Python

import json
import sys
import pygame
from pygame import RESIZABLE

from client import Client
from DiGraph import DiGraph
from GraphAlgo import GraphAlgo


def load_graph_and_algo(server_client: Client):
    graph_json = server_client.get_graph()
    json_obj = json.loads(graph_json)
    with open('curr_graph', 'w') as f:
        json.dump(json_obj, f)
    graph_algo = GraphAlgo()
    graph_algo.load_from_json('curr_graph')
    return graph_algo


def start_client():
    server_client = Client()
    port = 6666
    host = '127.0.0.1'
    server_client.start_connection(host, port)
    return server_client


if name == 'main':
    client = start_client()

    Algo = load_graph_and_algo(client)
    client.add_agent("{"id":0}")
    client.start()
    Algo.plot_graph(client)v
