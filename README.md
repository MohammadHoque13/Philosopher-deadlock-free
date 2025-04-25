# Philosopher-deadlock-free

#include <pthread.h>
#include <stdio.h>
#include <unistd.h>

pthread_mutex_t fork1 = PTHREAD_MUTEX_INITIALIZER;
pthread_mutex_t fork2 = PTHREAD_MUTEX_INITIALIZER;

void* philosopher0(void* arg) {
    while (1) {
        printf("Philosopher 0 is thinking...\n");
        sleep(1);
        
        
   pthread_mutex_lock(&fork1);
        pthread_mutex_lock(&fork2);
        
   printf("Philosopher 0 is eating...\n");
        sleep(1);
        
   pthread_mutex_unlock(&fork2);
        pthread_mutex_unlock(&fork1);
    }
    return NULL;
}

void* philosopher1(void* arg) {
    while (1) {
        printf("Philosopher 1 is thinking...\n");
        sleep(1);

   pthread_mutex_lock(&fork1);
        pthread_mutex_lock(&fork2);

  printf("Philosopher 1 is eating...\n");
     sleep(1);

   pthread_mutex_unlock(&fork2);
        pthread_mutex_unlock(&fork1);
    }
    return NULL;
}

int main() {
    pthread_t t0, t1;
    pthread_create(&t0, NULL, philosopher0, NULL);
    pthread_create(&t1, NULL, philosopher1, NULL);

   pthread_join(t0, NULL);
    pthread_join(t1, NULL);
    return 0;
}
