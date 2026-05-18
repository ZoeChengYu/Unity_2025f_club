using System.Collections;
using System.Collections.Generic;
using UnityEngine;

    public class MapSpawner : MonoBehaviour
    {
        public List<GameObject> maps;

        public float mapMoveSpeed = 5f;

        List<GameObject> spawnedMaps = new List<GameObject>();

        public static MapSpawner instance;

        public void Start()
        {
            instance = this;
        }

        public void SpawnMap()
        {
            if (!this.enabled) return; //stop spawning when this is inactive

            GameObject n_map = Instantiate(maps[Random.Range(0, maps.Count)], this.transform);
            spawnedMaps.Add(n_map);

        }

        public void DespawnMap(GameObject obj)
        {
            spawnedMaps.Remove(obj);
        }

        public void StopMoveMap()
        {
            foreach (var map in spawnedMaps)
            {
                map.GetComponent<MapMover>().stopMove = true;
            }
            this.enabled = false;
        }
    }

